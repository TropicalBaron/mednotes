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
  <div style="border: 1px solid var(--background-modifier-border); padding: 15px; border-radius: 8px; background-color: var(--background-secondary); max-width: 450px;">
    <h3 style="margin-top: 0; margin-bottom: 12px; font-size: 1.1em;">Calculadora de Idade Pediátrica</h3>
    
    <label style="display: block; margin-bottom: 8px; font-size: 0.9em;"><b>Data da Consulta Anterior:</b></label>
    <input type="date" id="data-consulta-anterior" style="width: 100%; padding: 6px; margin-bottom: 12px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">

    <label style="display: block; margin-bottom: 8px; font-size: 0.9em;"><b>Idade na Consulta Anterior:</b></label>
    <div style="display: flex; gap: 8px; margin-bottom: 12px;">
      <input type="number" id="anos" placeholder="Anos" min="0" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      <input type="number" id="meses" placeholder="Meses" min="0" max="11" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
      <input type="number" id="dias" placeholder="Dias" min="0" max="30" style="width: 33%; padding: 6px; border-radius: 4px; border: 1px solid var(--background-modifier-border); background-color: var(--background-primary); color: var(--text-normal);">
    </div>

    <label style="display: block; margin-bottom: 8px; font-size: 0.9em;"><b>Data da Consulta Atual:</b></label>
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

// Lógica de cálculo e determinação de faixa etária
container.querySelector("#btn-calcular").addEventListener("click", () => {
  const dataAnteriorVal = container.querySelector("#data-consulta-anterior").value;
  const dataAtualVal = container.querySelector("#data-consulta-atual").value;
  const anos = parseInt(container.querySelector("#anos").value) || 0;
  const meses = parseInt(container.querySelector("#meses").value) || 0;
  const dias = parseInt(container.querySelector("#dias").value) || 0;

  if (!dataAnteriorVal) {
    alert("Por favor, selecione a data da consulta anterior.");
    return;
  }
  if (!dataAtualVal) {
    alert("Por favor, selecione a data da consulta atual.");
    return;
  }

  // Estimar data de nascimento a partir da consulta anterior
  const dataAnterior = new Date(dataAnteriorVal);
  const dataNascimento = new Date(dataAnterior);
  dataNascimento.setFullYear(dataNascimento.getFullYear() - anos);
  dataNascimento.setMonth(dataNascimento.getMonth() - meses);
  dataNascimento.setDate(dataNascimento.getDate() - dias);

  // Calcular diferença entre a consulta atual e a data de nascimento estimada
  const dataAtual = new Date(dataAtualVal);
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
  let faixa = "";
  const totalDiasVida = Math.floor((dataAtual - dataNascimento) / (1000 * 60 * 60 * 24));

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
