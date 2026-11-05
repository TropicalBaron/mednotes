# Puericultura

## Anamnese

- **Identificação**: Nome, Idade, sexo, morbidades, medicações/suplementação em uso
- **QP**: Se não tiver queixa, Puericultura
- **HMA**: Além da QP investigar:
	- Perguntar sobre Alimentação (Lactente exclusivo? Uso de fórmula)
	- Perguntar sobre troca de fraldas (quantas, consistencia do cocô, aparecencia do xixi)
	- Perguntar sobre hábitos de sono (Hora de dormir, acordar, despertares noturno, padrão de cochilos, etc.)
- **HPP**
- **H. Gestacional**: Normalmente será vide primeira consulta
- **H. DNPM**: Olhar e anotar na caderneta
- **H. Vacinal**: Olhar na caderneta
- **Exame Físico**
	- *Temp.*: Temperatura Axilar
	- *ACV*: FC + Descrição das bulhas
	- *AR*: FR + SatO2 + Descrição dos Murmúrios
	- *Rinoscopia*: Se tiver rinoscópio
	- *Oroscopia*:
	- *Otoscopia*:
	- *Genital*: Rotina até a puberdade
- **Avaliação Antropométrica**
	- *Peso e Z*
	- *Ganho Ponderal*: Em g/dia desde a última consulta
	- *Altura e Z*
	- *IMC e Z*
	- *P. Cefálico e Z*
	- *Fontanela Anterior*
	- *Fontanela Posterior*
- **HDs da Pediatria**: Alimentar, Crescimento, DNPM, Vacinal e Clínico
- **CD**:

```dataviewjs
// Estilização do container
const container = dv.container;

container.innerHTML = `
  <div style="background-color: var(--background-secondary); padding: 15px; border-radius: 8px; border: 1px solid var(--background-modifier-border);">
    <h3 style="margin-top: 0; margin-bottom: 12px; font-size: 1.1em; text-align: center;">Calculadora de Idade Pediátrica</h3>

    <div style="margin-bottom: 12px; display: flex; gap: 10px;">
      <label style="font-size: 0.85em; cursor: pointer;">
        <input type="radio" name="modo-calculo" value="nascimento" checked> Data de Nascimento
      </label>
      <label style="font-size: 0.85em; cursor: pointer;">
        <input type="radio" name="modo-calculo" value="anterior"> Consulta Anterior
      </label>
    </div>

    <!-- MODO 1: Data de Nascimento -->
    <div id="secao-nascimento" style="margin-bottom: 12px;">
      <label style="display: block; margin-bottom: 4px; font-size: 0.9em;"><b>Data de Nascimento:</b></label>
      <input type="date" id="data-nascimento" style="width: 100%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
    </div>

    <!-- MODO 2: Consulta Anterior -->
    <div id="secao-anterior" style="display: none; margin-bottom: 12px;">
      <label style="display: block; margin-bottom: 4px; font-size: 0.9em;"><b>Data da Consulta Anterior:</b></label>
      <input type="date" id="data-consulta-anterior" style="width: 100%; padding: 6px; margin-bottom: 8px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">

      <label style="display: block; margin-bottom: 4px; font-size: 0.9em;"><b>Idade na Consulta Anterior:</b></label>
      <div style="display: flex; gap: 8px;">
        <input type="number" id="anos" placeholder="Anos" min="0" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
        <input type="number" id="meses" placeholder="Meses" min="0" max="11" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
        <input type="number" id="dias" placeholder="Dias" min="0" max="30" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      </div>
    </div>

    <label style="display: block; margin-bottom: 4px; font-size: 0.9em;"><b>Data da Consulta Atual:</b></label>
    <input type="date" id="data-consulta-atual" style="width: 100%; padding: 6px; margin-bottom: 15px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">

    <button id="btn-calcular" style="width: 100%; padding: 8px; border-radius: 4px; background-color: var(--interactive-accent); color: var(--text-on-accent); border: none; cursor: pointer; font-weight: bold; margin-bottom: 12px;">Calcular Idade Atual</button>

    <div id="resultado" style="display: none; padding: 10px; border-radius: 4px; background-color: var(--background-primary); border: 1px solid var(--background-modifier-border);">
      <p style="margin: 0 0 6px 0; font-size: 0.95em;"><b>Idade na Consulta Atual:</b> <span id="res-idade"></span></p>
      <p style="margin: 0; font-size: 0.95em;"><b>Faixa Etária:</b> <span id="res-faixa" style="font-weight: bold; color: var(--text-accent);"></span></p>
    </div>
  </div>
`;

// Preenche a data da consulta atual com a data de hoje automaticamente
const inputAtual = container.querySelector("#data-consulta-atual");
inputAtual.value = new Date().toISOString().split("T")[0];

// Controle de visibilidade dos modos de cálculo
const radioModos = container.querySelectorAll("input[name='modo-calculo']");
const secaoNascimento = container.querySelector("#secao-nascimento");
const secaoAnterior = container.querySelector("#secao-anterior");

radioModos.forEach(radio => {
  radio.addEventListener("change", (e) => {
    if (e.target.value === "nascimento") {
      secaoNascimento.style.display = "block";
      secaoAnterior.style.display = "none";
    } else {
      secaoNascimento.style.display = "none";
      secaoAnterior.style.display = "block";
    }
  });
});

// Lógica de cálculo e determinação de faixa etária
container.querySelector("#btn-calcular").addEventListener("click", () => {
  const modoAtivo = container.querySelector("input[name='modo-calculo']:checked").value;
  const dataAtualVal = container.querySelector("#data-consulta-atual").value;

  if (!dataAtualVal) {
    alert("Por favor, selecione a data da consulta atual.");
    return;
  }

  const [anoAtual, mesAtual, diaAtual] = dataAtualVal.split("-").map(Number);
  const dataAtual = new Date(anoAtual, mesAtual - 1, diaAtual);
  let dataNascimento;

  if (modoAtivo === "nascimento") {
    const dataNascVal = container.querySelector("#data-nascimento").value;
    if (!dataNascVal) {
      alert("Por favor, selecione a data de nascimento.");
      return;
    }
    const [anoNasc, mesNasc, diaNasc] = dataNascVal.split("-").map(Number);
    dataNascimento = new Date(anoNasc, mesNasc - 1, diaNasc);
  } else {
    const dataAnteriorVal = container.querySelector("#data-consulta-anterior").value;
    if (!dataAnteriorVal) {
      alert("Por favor, selecione a data da consulta anterior.");
      return;
    }

    const anos = parseInt(container.querySelector("#anos").value) || 0;
    const meses = parseInt(container.querySelector("#meses").value) || 0;
    const dias = parseInt(container.querySelector("#dias").value) || 0;

    const [anoAnt, mesAnt, diaAnt] = dataAnteriorVal.split("-").map(Number);
    const dataAnterior = new Date(anoAnt, mesAnt - 1, diaAnt);

    dataNascimento = new Date(dataAnterior);
    dataNascimento.setFullYear(dataNascimento.getFullYear() - anos);
    dataNascimento.setMonth(dataNascimento.getMonth() - meses);
    dataNascimento.setDate(dataNascimento.getDate() - dias);
  }

  // Calcular diferença exata de anos, meses e dias
  let diffAnos = dataAtual.getFullYear() - dataNascimento.getFullYear();
  let diffMeses = dataAtual.getMonth() - dataNascimento.getMonth();
  let diffDias = dataAtual.getDate() - dataNascimento.getDate();

  if (diffDias < 0) {
    diffMeses -= 1;
    const ultimoDiaMesAnterior = new Date(dataAtual.getFullYear(), dataAtual.getMonth(), 0).getDate();
    diffDias += ultimoDiaMesAnterior;
  }

  if (diffMeses < 0) {
    diffAnos -= 1;
    diffMeses += 12;
  }

  // Determinar Faixa Etária
  const totalDiasVida = Math.floor((dataAtual - dataNascimento) / (1000 * 60 * 60 * 24));
  let faixa = "";

  if (totalDiasVida < 0) {
    faixa = "Data inválida (consulta atual anterior ao nascimento)";
  } else if (totalDiasVida <= 28) {
    faixa = "Recém-nascido / Neonato";
  } else if (diffAnos < 2) {
    faixa = "Lactente";
  } else if (diffAnos < 6) {
    faixa = "Pré-escolar (Primeira Infância)";
  } else if (diffAnos < 10) {
    faixa = "Escolar (Segunda Infância)";
  } else if (diffAnos < 20) {
    faixa = "Adolescente";
  } else {
    faixa = "Adulto";
  }

  // Exibir resultados
  container.querySelector("#resultado").style.display = "block";
  container.querySelector("#res-idade").textContent = `${diffAnos} ano(s), ${diffMeses} mês(es) e ${diffDias} dia(s)`;
  container.querySelector("#res-faixa").textContent = faixa;
});
```

```dataviewjs
const container = dv.container;

// Tabela de Marcos do DNPM extraída e parametrizada por limite em dias
const esquemaDNPM = [
  {
    faixa: "0 a 1 Mês",
    limiteDias: 30,
    marcos: [
      { texto: "Postura flexionada de recém-nascido", alerta: false },
      { texto: "Observa o rosto de quem olha para ele", alerta: false },
      { texto: "Reage ao som de campainha/chocalho", alerta: false },
      { texto: "Ausência de reflexo de Moro", alerta: true },
      { texto: "Microcefalia ou Macrocefalia evidente", alerta: true }
    ]
  },
  {
    faixa: "1 a 2 Meses",
    limiteDias: 60,
    marcos: [
      { texto: "Eleva a cabeça momentaneamente em prono", alerta: false },
      { texto: "Sorriso social quando estimulado", alerta: false },
      { texto: "Emite sons/vocalizações curtas", alerta: false },
      { texto: "Acompanha objetos com o olhar até a linha média", alerta: false },
      { texto: "Hipotonia muscular acentuada", alerta: true }
    ]
  },
  {
    faixa: "2 a 4 Meses",
    limiteDias: 120,
    marcos: [
      { texto: "Sustenta a cabeça de forma firme ao estar sentado", alerta: false },
      { texto: "Responde ao contato verbal sorrindo/gorgolejando", alerta: false },
      { texto: "Abre as mãos espontaneamente e junta-as no centro", alerta: false },
      { texto: "Leva objetos voluntariamente à boca", alerta: false },
      { texto: "Assimetria postural persistente de membros", alerta: true }
    ]
  },
  {
    faixa: "4 a 6 Meses",
    limiteDias: 180,
    marcos: [
      { texto: "Rola de costas para o lado ou de bruços", alerta: false },
      { texto: "Alcança e pega brinquedos/objetos voluntariamente", alerta: false },
      { texto: "Muda a atenção ao ouvir o som do próprio nome", alerta: false },
      { texto: "Lalia e emite sílabas como 'da-da', 'ba-ba'", alerta: false },
      { texto: "Mãos continuamente fechadas com polegar aduto", alerta: true }
    ]
  },
  {
    faixa: "6 a 9 Meses",
    limiteDias: 270,
    marcos: [
      { texto: "Senta-se sozinho sem apoio de mãos", alerta: false },
      { texto: "Passa objetos de uma mão para a outra", alerta: false },
      { texto: "Realiza preensão radial ou em pinça inferior", alerta: false },
      { texto: "Estranha pessoas desconhecidas", alerta: false },
      { texto: "Não mantém o apoio do próprio peso nas pernas", alerta: true }
    ]
  },
  {
    faixa: "9 a 12 Meses",
    limiteDias: 365,
    marcos: [
      { texto: "Fica em pé segurando-se nos móveis", alerta: false },
      { texto: "Executa a preensão em pinça fina (polegar e indicador)", alerta: false },
      { texto: "Acena 'tchau' ou faz 'palminhas'", alerta: false },
      { texto: "Fala de 1 a 3 palavras com significado (ex: 'mamãe')", alerta: false },
      { texto: "Ausência de engatinhar ou arrastar eficiente", alerta: true }
    ]
  },
  {
    faixa: "12 a 15 Meses",
    limiteDias: 456,
    marcos: [
      { texto: "Carrega objetos enquanto caminha sem ajuda", alerta: false },
      { texto: "Coloca blocos em um recipiente/copo", alerta: false },
      { texto: "Aponta com o indicador para mostrar o que deseja", alerta: false },
      { texto: "Imita gestos simples de adultos em brincadeiras", alerta: false },
      { texto: "Incapacidade de andar sem apoio até 15 meses", alerta: true }
    ]
  },
  {
    faixa: "15 a 18 Meses",
    limiteDias: 547,
    marcos: [
      { texto: "Anda sozinho com bom equilíbrio", alerta: false },
      { texto: "Constrói torre com 3 a 4 cubos", alerta: false },
      { texto: "Vocabulário ativo de pelo menos 6 palavras", alerta: false },
      { texto: "Usa colher ou garfo levando comida à boca", alerta: false },
      { texto: "Não atende pelo nome ou evita contato visual", alerta: true }
    ]
  },
  {
    faixa: "18 a 24 Meses",
    limiteDias: 730,
    marcos: [
      { texto: "Corre e chuta uma bola mantendo o equilíbrio", alerta: false },
      { texto: "Junta 2 palavras para formar frases curtas (ex: 'quer água')", alerta: false },
      { texto: "Tira peças simples de vestuário sem ajuda", alerta: false },
      { texto: "Demonstra interesse por brincar com outras crianças", alerta: false },
      { texto: "Perda abrupta de habilidades de fala adquiridas", alerta: true }
    ]
  },
  {
    faixa: "2 a 3 Anos (24 a 36 Meses)",
    limiteDias: 1095,
    marcos: [
      { texto: "Pula com os dois pés juntos no mesmo lugar", alerta: false },
      { texto: "Desenha círculos ou linhas verticais em papel", alerta: false },
      { texto: "Forma frases completas de 3 a 4 palavras", alerta: false },
      { texto: "Veste roupas simples com supervisão", alerta: false },
      { texto: "Fala predominantemente ininteligível para estranhos", alerta: true }
    ]
  }
];

let htmlGrid = `
  <div style="background-color: var(--background-secondary); padding: 16px; border-radius: 8px; border: 1px solid var(--background-modifier-border);">
    <h3 style="margin-top: 0; margin-bottom: 12px; font-size: 1.1em; text-align: center;">Vigilância do Desenvolvimento Neuropsicomotor (DNPM)</h3>

    <label style="display: block; margin-bottom: 6px; font-size: 0.9em;"><b>Idade do Paciente:</b></label>
    <div style="display: flex; gap: 8px; margin-bottom: 12px;">
      <input type="number" id="dnpm-anos" placeholder="Anos" min="0" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      <input type="number" id="dnpm-meses" placeholder="Meses" min="0" max="11" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      <input type="number" id="dnpm-dias" placeholder="Dias" min="0" max="30" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
    </div>

    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px;">
      <span id="label-filtro-dnpm" style="font-size: 0.8em; color: var(--text-muted); font-weight: bold;">Exibindo: Todas as faixas do DNPM</span>
      <div style="display: flex; gap: 6px;">
        <button id="btn-dnpm-marcar" style="padding: 2px 6px; font-size: 0.75em; border-radius: 4px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-muted); cursor: pointer;">Checar Normais</button>
        <button id="btn-dnpm-limpar" style="padding: 2px 6px; font-size: 0.75em; border-radius: 4px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-muted); cursor: pointer;">Limpar</button>
      </div>
    </div>

    <div id="lista-dnpm-container" style="max-height: 400px; overflow-y: auto; padding-right: 6px; margin-bottom: 14px;">
`;

esquemaDNPM.forEach((grupo, gIdx) => {
  htmlGrid += `
    <div class="bloco-faixa-dnpm" data-dias="${grupo.limiteDias}" style="margin-bottom: 10px; background: var(--background-primary); padding: 8px 12px; border-radius: 6px; border: 1px solid var(--background-modifier-border);">
      <strong style="display: block; margin-bottom: 6px; font-size: 0.88em; color: var(--text-accent);">${grupo.faixa}</strong>
  `;

  grupo.marcos.forEach((m, mIdx) => {
    const id = `chk-dnpm-${gIdx}-${mIdx}`;
    const estiloAlerta = m.alerta ? "color: var(--text-error, #d32f2f); font-weight: bold;" : "";
    const tagAlerta = m.alerta ? " ⚠️ (Sinal de Alerta)" : "";

    htmlGrid += `
      <label style="display: flex; align-items: center; gap: 8px; font-size: 0.85em; margin-bottom: 4px; cursor: pointer; ${estiloAlerta}">
        <input type="checkbox" class="chk-dnpm-item" id="${id}" data-texto="${m.texto}" data-faixa="${grupo.faixa}" data-alerta="${m.alerta}" style="cursor: pointer;">
        <span>${m.texto}${tagAlerta}</span>
      </label>
    `;
  });

  htmlGrid += `</div>`;
});

htmlGrid += `
    </div>

    <button id="btn-verificar-dnpm" style="width: 100%; padding: 8px; border-radius: 4px; background-color: var(--interactive-accent); color: var(--text-on-accent); border: none; cursor: pointer; font-weight: bold; margin-bottom: 12px;">Avaliar Desenvolvimento</button>

    <div id="res-dnpm" style="display: none; padding: 12px; border-radius: 6px; background-color: var(--background-primary); border: 1px solid var(--background-modifier-border);">
      <p style="margin: 0 0 6px 0; font-size: 0.95em;"><b>Parecer DNPM:</b> <span id="status-dnpm-texto" style="font-weight: bold;"></span></p>
      <div id="detalhes-dnpm" style="margin-top: 8px; font-size: 0.85em; color: var(--text-muted);"></div>
    </div>
  </div>
`;

container.innerHTML = htmlGrid;

// Lógica de filtragem dinâmica pela idade
const inAnos = container.querySelector("#dnpm-anos");
const inMeses = container.querySelector("#dnpm-meses");
const inDias = container.querySelector("#dnpm-dias");
const labelFiltro = container.querySelector("#label-filtro-dnpm");
const blocosFaixa = container.querySelectorAll(".bloco-faixa-dnpm");

function atualizarFiltroDNPM() {
  const valAnos = inAnos.value.trim();
  const valMeses = inMeses.value.trim();
  const valDias = inDias.value.trim();

  if (valAnos === "" && valMeses === "" && valDias === "") {
    blocosFaixa.forEach(b => b.style.display = "block");
    labelFiltro.textContent = "Exibindo: Todas as faixas do DNPM";
    return;
  }

  const anos = parseInt(valAnos) || 0;
  const meses = parseInt(valMeses) || 0;
  const dias = parseInt(valDias) || 0;

  const totalDiasPaciente = (anos * 365) + (meses * 30.4375) + dias;

  labelFiltro.textContent = `Exibindo: Marcos esperados até ${anos}a ${meses}m ${dias}d`;

  blocosFaixa.forEach(bloco => {
    const limite = parseFloat(bloco.getAttribute("data-dias"));
    if (limite <= totalDiasPaciente) {
      bloco.style.display = "block";
    } else {
      bloco.style.display = "none";
    }
  });
}

[inAnos, inMeses, inDias].forEach(input => {
  input.addEventListener("input", atualizarFiltroDNPM);
});

// Ações auxiliares para preenchimento rápido
container.querySelector("#btn-dnpm-marcar").addEventListener("click", () => {
  blocosFaixa.forEach(b => {
    if (b.style.display !== "none") {
      b.querySelectorAll(".chk-dnpm-item").forEach(c => {
        if (c.getAttribute("data-alerta") !== "true") {
          c.checked = true;
        }
      });
    }
  });
});

container.querySelector("#btn-dnpm-limpar").addEventListener("click", () => {
  container.querySelectorAll(".chk-dnpm-item").forEach(c => c.checked = false);
});

// Lógica de avaliação clínica final do DNPM
container.querySelector("#btn-verificar-dnpm").addEventListener("click", () => {
  const pendentesNormais = [];
  const alertasMarcados = [];

  blocosFaixa.forEach(bloco => {
    if (bloco.style.display !== "none") {
      const chks = bloco.querySelectorAll(".chk-dnpm-item");
      chks.forEach(chk => {
        const isAlerta = chk.getAttribute("data-alerta") === "true";
        const texto = chk.getAttribute("data-texto");
        const faixa = chk.getAttribute("data-faixa");

        if (isAlerta && chk.checked) {
          alertasMarcados.push({ texto, faixa });
        } else if (!isAlerta && !chk.checked) {
          pendentesNormais.push({ texto, faixa });
        }
      });
    }
  });

  const resDiv = container.querySelector("#res-dnpm");
  const statusSpan = container.querySelector("#status-dnpm-texto");
  const detalhesDiv = container.querySelector("#detalhes-dnpm");

  resDiv.style.display = "block";

  if (alertasMarcados.length > 0) {
    statusSpan.textContent = "🚨 SINAL DE ALERTA / RISCO NO DESENVOLVIMENTO";
    statusSpan.style.color = "var(--text-error, #d32f2f)";

    let html = "<b style='color: var(--text-normal);'>Sinais de Alerta identificados:</b><ul style='margin: 4px 0 6px 16px; padding: 0;'>";
    alertasMarcados.forEach(a => {
      html += `<li><b>${a.faixa}:</b> ${a.texto}</li>`;
    });
    html += "</ul>";

    if (pendentesNormais.length > 0) {
      html += "<b style='color: var(--text-normal);'>Marcos normais ausentes:</b><ul style='margin: 4px 0 0 16px; padding: 0;'>";
      pendentesNormais.forEach(p => {
        html += `<li><b>${p.faixa}:</b> ${p.texto}</li>`;
      });
      html += "</ul>";
    }

    detalhesDiv.innerHTML = html;
  } else if (pendentesNormais.length === 0) {
    statusSpan.textContent = "DESENVOLVIMENTO ADEQUADO ✅";
    statusSpan.style.color = "var(--text-success, #2e7d32)";
    detalhesDiv.innerHTML = "Todos os marcos esperados para a idade informada foram alcançados e não há sinais de alerta marcados.";
  } else {
    statusSpan.textContent = `PROVÁVEL ATRASO NO DESENVOLVIMENTO ⚠️ (${pendentesNormais.length} marco(s) ausente(s))`;
    statusSpan.style.color = "var(--text-warning, #f39c12)";

    let html = "<b style='color: var(--text-normal);'>Marcos esperados não alcançados:</b><ul style='margin: 4px 0 0 16px; padding: 0;'>";
    pendentesNormais.forEach(p => {
      html += `<li><b>${p.faixa}:</b> ${p.texto}</li>`;
    });
    html += "</ul>";
    detalhesDiv.innerHTML = html;
  }
});
```

```dataviewjs
const container = dv.container;

// Tabela de idades limites em dias para o filtro automático
const esquemaVacinal = [
  {
    faixa: "Ao Nascer",
    limiteDias: 0,
    vacinas: ["BCG", "Hepatite B"]
  },
  {
    faixa: "2 Meses",
    limiteDias: 60,
    vacinas: ["Pentavalente", "VIP (Pólio inativada)", "Rotavírus", "Pneumocócica 20V"]
  },
  {
    faixa: "3 Meses",
    limiteDias: 90,
    vacinas: ["Meningocócica C"]
  },
  {
    faixa: "4 Meses",
    limiteDias: 120,
    vacinas: ["Pentavalente", "VIP (Pólio inativada)", "Rotavírus", "Pneumocócica 10V"]
  },
  {
    faixa: "5 Meses",
    limiteDias: 150,
    vacinas: ["Meningocócica C"]
  },
  {
    faixa: "6 Meses",
    limiteDias: 180,
    vacinas: ["Pentavalente", "VIP (Pólio inativada)", "Covid-19"]
  },
  {
    faixa: "7 Meses",
    limiteDias: 210,
    vacinas: ["Covid-19"]
  },
  {
    faixa: "9 Meses",
    limiteDias: 270,
    vacinas: ["Febre Amarela", "Covid-19 (se for Pfizer)"]
  },
  {
    faixa: "1 Ano (12 Meses)",
    limiteDias: 365,
    vacinas: ["SCR (Tríplice Viral)", "Pneumocócica 20V", "Meningocócica ACWY"]
  },
  {
    faixa: "1 Ano e 3 Meses (15 Meses)",
    limiteDias: 456,
    vacinas: ["DTP", "VIP (Pólio inativada)", "Tetraviral", "Hepatite A"]
  },
  {
    faixa: "4 Anos",
    limiteDias: 1460,
    vacinas: ["DTP", "VIP (Pólio inativada)", "Varicela", "Febre Amarela"]
  },
  {
    faixa: "Adolescentes (11 a 19 anos)",
    limiteDias: 4015, // ~11 anos
    vacinas: [
      "Meningo ACWY (11 a 14 anos)",
      "HPV (9 a 14 anos)",
      "Qdenga (10 a 14 anos)",
      "HPV (9 a 14 anos + Vítima de Abuso [0-6m])",
      "dT (Reforço a cada 10 anos)"
    ]
  },
  {
    faixa: "Adultos (20 a 59 anos)",
    limiteDias: 7300, // 20 anos
    vacinas: [
      "dT (Reforço a cada 10 anos)",
      "HPV (9 a 45 anos em situação de risco [0-2-6m])"
    ]
  },
  {
    faixa: "Idosos (60+ anos)",
    limiteDias: 21915, // 60 anos
    vacinas: ["dT (Reforço a cada 10 anos)"]
  },
  {
    faixa: "Gestantes / Especiais / Anual",
    limiteDias: -1, // Sempre disponível se não filtrar por idade estrita
    vacinas: [
      "dTpa (20ª a 36ª semana de gestação)",
      "VSR (28ª a 36ª semana de gestação)",
      "Influenza (Anual - Crianças 6m-5a, Gestantes, Idosos, Indígenas e Grupos de risco)"
    ]
  }
];

let htmlGrid = `
  <div style="background-color: var(--background-secondary); padding: 16px; border-radius: 8px; border: 1px solid var(--background-modifier-border);">
    <h3 style="margin-top: 0; margin-bottom: 12px; font-size: 1.1em; text-align: center;">Avaliação Vacinal Pediátrica e Adulto</h3>

    <label style="display: block; margin-bottom: 6px; font-size: 0.9em;"><b>Idade do Paciente:</b></label>
    <div style="display: flex; gap: 8px; margin-bottom: 12px;">
      <input type="number" id="v-anos" placeholder="Anos" min="0" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      <input type="number" id="v-meses" placeholder="Meses" min="0" max="11" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      <input type="number" id="v-dias" placeholder="Dias" min="0" max="30" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
    </div>

    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px;">
      <span id="label-filtro" style="font-size: 0.8em; color: var(--text-muted); font-weight: bold;">Exibindo: Todas as faixas etárias</span>
      <div style="display: flex; gap: 6px;">
        <button id="btn-vac-todas" style="padding: 2px 6px; font-size: 0.75em; border-radius: 4px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-muted); cursor: pointer;">Checar Todas</button>
        <button id="btn-vac-limpar" style="padding: 2px 6px; font-size: 0.75em; border-radius: 4px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-muted); cursor: pointer;">Limpar</button>
      </div>
    </div>

    <div id="lista-vacinas-container" style="max-height: 380px; overflow-y: auto; padding-right: 6px; margin-bottom: 14px;">
`;

esquemaVacinal.forEach((grupo, gIdx) => {
  htmlGrid += `
    <div class="bloco-faixa-vacinal" data-dias="${grupo.limiteDias}" style="margin-bottom: 10px; background: var(--background-primary); padding: 8px 12px; border-radius: 6px; border: 1px solid var(--background-modifier-border);">
      <strong style="display: block; margin-bottom: 6px; font-size: 0.88em; color: var(--text-accent);">${grupo.faixa}</strong>
  `;

  grupo.vacinas.forEach((vacina, vIdx) => {
    const id = `chk-v-${gIdx}-${vIdx}`;
    htmlGrid += `
      <label style="display: flex; align-items: center; gap: 8px; font-size: 0.85em; margin-bottom: 4px; cursor: pointer;">
        <input type="checkbox" class="chk-vacina-item" id="${id}" data-nome="${vacina}" data-faixa="${grupo.faixa}" style="cursor: pointer;">
        <span>${vacina}</span>
      </label>
    `;
  });

  htmlGrid += `</div>`;
});

htmlGrid += `
    </div>

    <button id="btn-verificar-esquema" style="width: 100%; padding: 8px; border-radius: 4px; background-color: var(--interactive-accent); color: var(--text-on-accent); border: none; cursor: pointer; font-weight: bold; margin-bottom: 12px;">Verificar Caderneta</button>

    <div id="res-vacinacao" style="display: none; padding: 12px; border-radius: 6px; background-color: var(--background-primary); border: 1px solid var(--background-modifier-border);">
      <p style="margin: 0 0 6px 0; font-size: 0.95em;"><b>Status Vacinal:</b> <span id="status-vac-texto" style="font-weight: bold;"></span></p>
      <div id="detalhes-vac-pendentes" style="margin-top: 8px; font-size: 0.85em; color: var(--text-muted);"></div>
    </div>
  </div>
`;

container.innerHTML = htmlGrid;

// Lógica de filtragem dinâmica pela idade digitada
const inAnos = container.querySelector("#v-anos");
const inMeses = container.querySelector("#v-meses");
const inDias = container.querySelector("#v-dias");
const labelFiltro = container.querySelector("#label-filtro");
const blocosFaixa = container.querySelectorAll(".bloco-faixa-vacinal");

function atualizarFiltroVacinas() {
  const valAnos = inAnos.value.trim();
  const valMeses = inMeses.value.trim();
  const valDias = inDias.value.trim();

  // Se nenhum campo foi preenchido, mostra tudo por padrão
  if (valAnos === "" && valMeses === "" && valDias === "") {
    blocosFaixa.forEach(b => b.style.display = "block");
    labelFiltro.textContent = "Exibindo: Todas as faixas etárias";
    return;
  }

  const anos = parseInt(valAnos) || 0;
  const meses = parseInt(valMeses) || 0;
  const dias = parseInt(valDias) || 0;

  const totalDiasPaciente = (anos * 365) + (meses * 30.4375) + dias;

  labelFiltro.textContent = `Exibindo: Vacinas indicadas até ${anos}a ${meses}m ${dias}d`;

  blocosFaixa.forEach(bloco => {
    const limite = parseFloat(bloco.getAttribute("data-dias"));
    // Mostra apenas faixas etárias com limite em dias menor ou igual à idade do paciente
    if (limite === -1 || limite <= totalDiasPaciente) {
      bloco.style.display = "block";
    } else {
      bloco.style.display = "none";
    }
  });
}

[inAnos, inMeses, inDias].forEach(input => {
  input.addEventListener("input", atualizarFiltroVacinas);
});

// Botões auxiliares
container.querySelector("#btn-vac-todas").addEventListener("click", () => {
  blocosFaixa.forEach(b => {
    if (b.style.display !== "none") {
      b.querySelectorAll(".chk-vacina-item").forEach(c => c.checked = true);
    }
  });
});

container.querySelector("#btn-vac-limpar").addEventListener("click", () => {
  container.querySelectorAll(".chk-vacina-item").forEach(c => c.checked = false);
});

// Lógica de verificação final
container.querySelector("#btn-verificar-esquema").addEventListener("click", () => {
  const pendencias = [];

  // Considera apenas as vacinas visíveis conforme o filtro de idade
  blocosFaixa.forEach(bloco => {
    if (bloco.style.display !== "none") {
      const chks = bloco.querySelectorAll(".chk-vacina-item");
      chks.forEach(chk => {
        if (!chk.checked) {
          pendencias.push({
            vacina: chk.getAttribute("data-nome"),
            faixa: chk.getAttribute("data-faixa")
          });
        }
      });
    }
  });

  const resDiv = container.querySelector("#res-vacinacao");
  const statusSpan = container.querySelector("#status-vac-texto");
  const detalhesDiv = container.querySelector("#detalhes-vac-pendentes");

  resDiv.style.display = "block";

  if (pendencias.length === 0) {
    statusSpan.textContent = "VACINAÇÃO EM DIA ✅";
    statusSpan.style.color = "var(--text-success, #2e7d32)";
    detalhesDiv.innerHTML = "Todas as vacinas esperadas para a idade foram marcadas como administradas.";
  } else {
    statusSpan.textContent = `VACINAÇÃO PENDENTE ⚠️ (${pendencias.length} dose(s) faltante(s))`;
    statusSpan.style.color = "var(--text-error, #d32f2f)";

    let htmlPendencias = "<b style='color: var(--text-normal);'>Doses pendentes para a faixa etária:</b><ul style='margin: 4px 0 0 16px; padding: 0;'>";
    pendencias.forEach(p => {
      htmlPendencias += `<li><b>${p.faixa}:</b> ${p.vacina}</li>`;
    });
    htmlPendencias += "</ul>";
    detalhesDiv.innerHTML = htmlPendencias;
  }
});
```



```dataviewjs
// Estilização do container
const container = dv.container;
container.innerHTML = `
  <div style="border: 1px solid var(--background-modifier-border); padding: 15px; border-radius: 8px; background-color: var(--background-secondary); max-width: 480px;">
    <h3 style="margin-top: 0; margin-bottom: 12px; font-size: 1.1em;">Calculadora de Ganho Ponderal Pediátrico</h3>
    
    <!-- Consulta Anterior -->
    <div style="display: flex; gap: 8px; margin-bottom: 8px;">
      <div style="flex: 1;">
        <label style="display: block; margin-bottom: 4px; font-size: 0.85em;"><b>Data Consulta Anterior:</b></label>
        <input type="date" id="data-ant" style="width: 100%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      </div>
      <div style="flex: 1;">
        <label style="display: block; margin-bottom: 4px; font-size: 0.85em;"><b>Peso Anterior (kg):</b></label>
        <input type="number" step="0.001" id="peso-ant" placeholder="Ex: 3.500" style="width: 100%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      </div>
    </div>

    <!-- Idade na Consulta Anterior -->
    <label style="display: block; margin-bottom: 4px; font-size: 0.85em;"><b>Idade na Consulta Anterior:</b></label>
    <div style="display: flex; gap: 8px; margin-bottom: 12px;">
      <input type="number" id="anos" placeholder="Anos" min="0" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      <input type="number" id="meses" placeholder="Meses" min="0" max="11" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      <input type="number" id="dias" placeholder="Dias" min="0" max="30" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
    </div>

    <!-- Consulta Atual -->
    <div style="display: flex; gap: 8px; margin-bottom: 15px;">
      <div style="flex: 1;">
        <label style="display: block; margin-bottom: 4px; font-size: 0.85em;"><b>Data Consulta Atual:</b></label>
        <input type="date" id="data-atual" style="width: 100%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      </div>
      <div style="flex: 1;">
        <label style="display: block; margin-bottom: 4px; font-size: 0.85em;"><b>Peso Atual (kg):</b></label>
        <input type="number" step="0.001" id="peso-atual" placeholder="Ex: 4.200" style="width: 100%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      </div>
    </div>

    <button id="btn-calcular-ponderal" style="width: 100%; padding: 8px; border-radius: 4px; background-color: var(--interactive-accent); color: var(--text-on-accent); border: none; cursor: pointer; font-weight: bold; margin-bottom: 12px;">Calcular Ganho Ponderal</button>

    <!-- Resultados -->
    <div id="resultado-ponderal" style="display: none; padding: 10px; border-radius: 4px; background-color: var(--background-primary); border: 1px solid var(--background-modifier-border);">
      <p style="margin: 0 0 4px 0; font-size: 0.9em;"><b>Intervalo entre consultas:</b> <span id="res-dias-intervalo"></span> dias</p>
      <p style="margin: 0 0 4px 0; font-size: 0.9em;"><b>Ganho Total de Peso:</b> <span id="res-ganho-total"></span></p>
      <p style="margin: 0 0 4px 0; font-size: 0.9em;"><b>Ganho Diário Real:</b> <span id="res-ganho-diario" style="font-weight: bold;"></span></p>
      <hr style="margin: 8px 0; border: 0; border-top: 1px solid var(--background-modifier-border);">
      <p style="margin: 0 0 4px 0; font-size: 0.9em;"><b>Faixa de Idade Média:</b> <span id="res-faixa-idade"></span></p>
      <p style="margin: 0; font-size: 0.9em;"><b>Ganho Esperado (Referência):</b> <span id="res-ganho-esperado" style="font-weight: bold; color: var(--text-accent);"></span></p>
    </div>
  </div>
`;

// Preenche a data da consulta atual com a data de hoje por padrão
const inputAtualDate = container.querySelector("#data-atual");
inputAtualDate.value = new Date().toISOString().split("T")[0];

container.querySelector("#btn-calcular-ponderal").addEventListener("click", () => {
  const dAntVal = container.querySelector("#data-ant").value;
  const dAtualVal = container.querySelector("#data-atual").value;
  const pAnt = parseFloat(container.querySelector("#peso-ant").value);
  const pAtual = parseFloat(container.querySelector("#peso-atual").value);
  const anos = parseInt(container.querySelector("#anos").value) || 0;
  const meses = parseInt(container.querySelector("#meses").value) || 0;
  const dias = parseInt(container.querySelector("#dias").value) || 0;

  if (!dAntVal || !dAtualVal) {
    alert("Por favor, preencha as datas de ambas as consultas.");
    return;
  }
  if (isNaN(pAnt) || isNaN(pAtual)) {
    alert("Por favor, informe os pesos registrados nas duas consultas.");
    return;
  }

  const dAnt = new Date(dAntVal);
  const dAtual = new Date(dAtualVal);
  const diffTempo = dAtual - dAnt;
  const diasIntervalo = Math.round(diffTempo / (1000 * 60 * 60 * 24));

  if (diasIntervalo <= 0) {
    alert("A data atual deve ser posterior à data da consulta anterior.");
    return;
  }

  // Estimar data de nascimento
  const dataNascimento = new Date(dAnt);
  dataNascimento.setFullYear(dataNascimento.getFullYear() - anos);
  dataNascimento.setMonth(dataNascimento.getMonth() - meses);
  dataNascimento.setDate(dataNascimento.getDate() - dias);

  // Idade média em dias no ponto central do intervalo de acompanhamento
  const metadeIntervalo = new Date(dAnt.getTime() + diffTempo / 2);
  const idadeMediaDias = Math.floor((metadeIntervalo - dataNascimento) / (1000 * 60 * 60 * 24));
  const idadeMediaMeses = idadeMediaDias / 30.4375;

  // Cálculo do ganho de peso
  const ganhoTotalKg = pAtual - pAnt;
  const ganhoTotalG = ganhoTotalKg * 1000;
  const ganhoDiarioG = ganhoTotalG / diasIntervalo;

  // Tabela de referência de Ganho Ponderal Padrão (OMS / SBP)
  let faixaTexto = "";
  let esperadoTexto = "";

  if (idadeMediaDias <= 28) {
    faixaTexto = "Neonato (0 a 28 dias)";
    esperadoTexto = "25 a 30 g/dia";
  } else if (idadeMediaMeses <= 3) {
    faixaTexto = "Lactente (1º ao 3º mês)";
    esperadoTexto = "25 a 30 g/dia (~700-900 g/mês)";
  } else if (idadeMediaMeses <= 6) {
    faixaTexto = "Lactente (4º ao 6º mês)";
    esperadoTexto = "20 a 25 g/dia (~500-600 g/mês)";
  } else if (idadeMediaMeses <= 9) {
    faixaTexto = "Lactente (7º ao 9º mês)";
    esperadoTexto = "15 a 20 g/dia (~400-500 g/mês)";
  } else if (idadeMediaMeses <= 12) {
    faixaTexto = "Lactente (10º ao 12º mês)";
    esperadoTexto = "10 a 15 g/dia (~250-300 g/mês)";
  } else if (idadeMediaMeses <= 24) {
    faixaTexto = "Lactente (1 a 2 anos)";
    esperadoTexto = "5 a 8 g/dia (~2 kg/ano)";
  } else if (idadeMediaMeses <= 60) {
    faixaTexto = "Pré-escolar (2 a 5 anos)";
    esperadoTexto = "5 a 6 g/dia (~2 kg/ano)";
  } else if (idadeMediaMeses <= 120) {
    faixaTexto = "Escolar (6 a 10 anos)";
    esperadoTexto = "5 a 9 g/dia (~2 a 3 kg/ano)";
  } else {
    faixaTexto = "Adolescente (> 10 anos)";
    esperadoTexto = "Varia com o estirão puberal (~3 a 7 kg/ano)";
  }

  // Exibição dos dados
  container.querySelector("#resultado-ponderal").style.display = "block";
  container.querySelector("#res-dias-intervalo").textContent = diasIntervalo;
  container.querySelector("#res-ganho-total").textContent = `${ganhoTotalKg >= 0 ? "+" : ""}${ganhoTotalG.toFixed(0)} g (${ganhoTotalKg.toFixed(3)} kg)`;
  container.querySelector("#res-ganho-diario").textContent = `${ganhoDiarioG.toFixed(1)} g/dia`;
  container.querySelector("#res-faixa-idade").textContent = faixaTexto;
  container.querySelector("#res-ganho-esperado").textContent = esperadoTexto;
});
```

```dataviewjs
// Estilização do container
const container = dv.container;
container.innerHTML = `
  <div style="border: 1px solid var(--background-modifier-border); padding: 15px; border-radius: 8px; background-color: var(--background-secondary); max-width: 480px;">
    <h3 style="margin-top: 0; margin-bottom: 12px; font-size: 1.1em;">Calculadora de IMC Pediátrico</h3>
    
    <!-- Dados do Paciente -->
    <div style="display: flex; gap: 8px; margin-bottom: 8px;">
      <div style="flex: 1;">
        <label style="display: block; margin-bottom: 4px; font-size: 0.85em;"><b>Sexo do Paciente:</b></label>
        <select id="sexo" style="width: 100%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
          <option value="M">Masculino</option>
          <option value="F">Feminino</option>
        </select>
      </div>
      <div style="flex: 1;">
        <label style="display: block; margin-bottom: 4px; font-size: 0.85em;"><b>Data Consulta Anterior:</b></label>
        <input type="date" id="data-ant" style="width: 100%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      </div>
    </div>

    <!-- Idade na Consulta Anterior -->
    <label style="display: block; margin-bottom: 4px; font-size: 0.85em;"><b>Idade na Consulta Anterior:</b></label>
    <div style="display: flex; gap: 8px; margin-bottom: 8px;">
      <input type="number" id="anos" placeholder="Anos" min="0" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      <input type="number" id="meses" placeholder="Meses" min="0" max="11" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      <input type="number" id="dias" placeholder="Dias" min="0" max="30" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
    </div>

    <!-- Consulta Atual -->
    <div style="display: flex; gap: 8px; margin-bottom: 12px;">
      <div style="flex: 1;">
        <label style="display: block; margin-bottom: 4px; font-size: 0.85em;"><b>Data Consulta Atual:</b></label>
        <input type="date" id="data-atual" style="width: 100%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      </div>
      <div style="flex: 1;">
        <label style="display: block; margin-bottom: 4px; font-size: 0.85em;"><b>Peso Atual (kg):</b></label>
        <input type="number" step="0.001" id="peso-atual" placeholder="Ex: 14.5" style="width: 100%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      </div>
    </div>

    <div style="margin-bottom: 15px;">
      <label style="display: block; margin-bottom: 4px; font-size: 0.85em;"><b>Estatura/Comprimento Atual (cm):</b></label>
      <input type="number" step="0.1" id="estatura-atual" placeholder="Ex: 98.5" style="width: 100%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
    </div>

    <button id="btn-calcular-imc" style="width: 100%; padding: 8px; border-radius: 4px; background-color: var(--interactive-accent); color: var(--text-on-accent); border: none; cursor: pointer; font-weight: bold; margin-bottom: 12px;">Calcular IMC e Diagnóstico</button>

    <!-- Resultados -->
    <div id="resultado-imc" style="display: none; padding: 10px; border-radius: 4px; background-color: var(--background-primary); border: 1px solid var(--background-modifier-border);">
      <p style="margin: 0 0 4px 0; font-size: 0.9em;"><b>Idade na Consulta Atual:</b> <span id="res-idade-atual"></span></p>
      <p style="margin: 0 0 4px 0; font-size: 0.9em;"><b>IMC Calculado:</b> <span id="res-imc-val" style="font-weight: bold;"></span> kg/m²</p>
      <hr style="margin: 8px 0; border: 0; border-top: 1px solid var(--background-modifier-border);">
      <p style="margin: 0 0 4px 0; font-size: 0.9em;"><b>Classificação Antropométrica (OMS):</b></p>
      <p id="res-classificacao" style="margin: 0; font-weight: bold; font-size: 1em; color: var(--text-accent);"></p>
    </div>
  </div>
`;

// Preenche a data da consulta atual com a data de hoje por padrão
const inputAtualDate = container.querySelector("#data-atual");
inputAtualDate.value = new Date().toISOString().split("T")[0];

container.querySelector("#btn-calcular-imc").addEventListener("click", () => {
  const dAntVal = container.querySelector("#data-ant").value;
  const dAtualVal = container.querySelector("#data-atual").value;
  const peso = parseFloat(container.querySelector("#peso-atual").value);
  const estaturaCm = parseFloat(container.querySelector("#estatura-atual").value);
  const anos = parseInt(container.querySelector("#anos").value) || 0;
  const meses = parseInt(container.querySelector("#meses").value) || 0;
  const dias = parseInt(container.querySelector("#dias").value) || 0;

  if (!dAntVal || !dAtualVal) {
    alert("Por favor, preencha as datas de ambas as consultas.");
    return;
  }
  if (isNaN(peso) || peso <= 0 || isNaN(estaturaCm) || estaturaCm <= 0) {
    alert("Por favor, informe valores válidos para peso e estatura.");
    return;
  }

  const dAnt = new Date(dAntVal);
  const dAtual = new Date(dAtualVal);

  // Estimar data de nascimento
  const dataNascimento = new Date(dAnt);
  dataNascimento.setFullYear(dataNascimento.getFullYear() - anos);
  dataNascimento.setMonth(dataNascimento.getMonth() - meses);
  dataNascimento.setDate(dataNascimento.getDate() - dias);

  // Calcular idade na consulta atual
  let diffAnos = dAtual.getFullYear() - dataNascimento.getFullYear();
  let diffMeses = dAtual.getMonth() - dataNascimento.getMonth();
  let diffDias = dAtual.getDate() - dataNascimento.getDate();

  if (diffDias < 0) {
    diffMeses -= 1;
    const ultimoDiaMesAnterior = new Date(dAtual.getFullYear(), dAtual.getMonth(), 0).getDate();
    diffDias += ultimoDiaMesAnterior;
  }
  if (diffMeses < 0) {
    diffAnos -= 1;
    diffMeses += 12;
  }

  // Cálculo do IMC (kg/m²)
  const estaturaM = estaturaCm / 100;
  const imc = peso / (estaturaM * estaturaM);

  // Determinar a classificação nutricional pediátrica por faixa etária
  let diagnostico = "";
  
  if (diffAnos < 5) {
    // Referência OMS 0 a 5 anos (IMC para Idade)
    if (imc < 13.0) {
      diagnostico = "Magreza Acentuada (Escore-Z < -3)";
    } else if (imc < 14.0) {
      diagnostico = "Magreza (Escore-Z entre -3 e -2)";
    } else if (imc <= 17.0) {
      diagnostico = "Eutrofia (Escore-Z entre -2 e +1)";
    } else if (imc <= 18.0) {
      diagnostico = "Risco de Sobrepeso (Escore-Z entre +1 e +2)";
    } else if (imc <= 19.0) {
      diagnostico = "Sobrepeso (Escore-Z entre +2 e +3)";
    } else {
      diagnostico = "Obesidade (Escore-Z > +3)";
    }
  } else if (diffAnos < 10) {
    // Referência OMS 5 a 10 anos
    if (imc < 13.0) {
      diagnostico = "Magreza Acentuada (Escore-Z < -3)";
    } else if (imc < 14.5) {
      diagnostico = "Magreza (Escore-Z entre -3 e -2)";
    } else if (imc <= 18.0) {
      diagnostico = "Eutrofia (Escore-Z entre -2 e +1)";
    } else if (imc <= 20.0) {
      diagnostico = "Sobrepeso (Escore-Z entre +1 e +2)";
    } else if (imc <= 22.5) {
      diagnostico = "Obesidade (Escore-Z entre +2 e +3)";
    } else {
      diagnostico = "Obesidade Grave (Escore-Z > +3)";
    }
  } else {
    // Referência OMS 10 a 19 anos (Adolescentes)
    if (imc < 14.5) {
      diagnostico = "Magreza Acentuada (Escore-Z < -3)";
    } else if (imc < 16.0) {
      diagnostico = "Magreza (Escore-Z entre -3 e -2)";
    } else if (imc <= 22.5) {
      diagnostico = "Eutrofia (Escore-Z entre -2 e +1)";
    } else if (imc <= 26.0) {
      diagnostico = "Sobrepeso (Escore-Z entre +1 e +2)";
    } else if (imc <= 29.5) {
      diagnostico = "Obesidade (Escore-Z entre +2 e +3)";
    } else {
      diagnostico = "Obesidade Grave (Escore-Z > +3)";
    }
  }

  // Exibição dos resultados
  container.querySelector("#resultado-imc").style.display = "block";
  container.querySelector("#res-idade-atual").textContent = `${diffAnos} ano(s), ${diffMeses} mês(es) e ${diffDias} dia(s)`;
  container.querySelector("#res-imc-val").textContent = imc.toFixed(2);
  container.querySelector("#res-classificacao").textContent = diagnostico;
});
```

