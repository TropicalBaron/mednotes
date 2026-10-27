# Assistência Pré-Natal

- **Consultas Mínimas**
	- *IG <= 28 semanas*: 0s, 4s, 8s, 12s, 16s, 20s, 24s, 28s (consultas mensais)
	- *IG 28-36 semanas*: Consultas à cada 15 dias
	- *IG >36 semanas*: Consultas Semanais
	- *No puerpério (pós-parto)* Precoce + Tardia
		- Precoce: até 7 dias pós-parto
		- Tardia: até 42 dias pós-parto
- **Exame Físico Específico**
	- *Estática Fetal - Manobras de Leopold*: Apenas a partir das 34s (3º triméstre)
	- *Aferir BCF*: A partir da 12s-16s (teoricamente a partir das 10s já dá, mas é mto dificil)
	- *Peso*:A partir das 12s
- **Suplementações de Rotina**
	- *Ácido Fólico 400mcg* Desde 3m antes de engravidar até o fim da gestação
		- *Casos especiais -> Fazer 4mg/dia*:
			- História familiar de defeitos no tubo neural
			- Uso de anticonvulsivantes ou metotrexato
			- DM insulinodependente
			- Obesidade (IMC > 35)
			- Sindromes disabsortivas
			- Mutações da MTHFR
	- *Ferro 40-60mg de Elementar/dia* Desde o inicio da gravidez até 3m pós-parto o pós-abortamento
	- *Cálcio 500mg-1g/dia*: Apenas se baixa ingesta ou alto-risco de Pré-Eclampsia, ver [[Distúrbios Hipertensívos na Gestação#3. Pré-Eclâmpsia (PE)]]
- **Vacinação Recomendada**
	- *Influenza*: Dose única durante a campanha anual em qualquer IG
	- *dTPa (difiteria, tetano e coqueluche)* 20-36 semanas
		- Indicada para toda gestante em toda gestação entre 20-36 semanas
		- Lembrar que 1 dose dela vale tbm uma dose da dT
	- *dT (difiteria e tetano)*: A meta é ter 2 dT + 1 dTPa, confira o cartão de vacinação da gestante para ver se ela tomou na infância ou algum momento da vida as 2 doses de dT, se não ou não for possível complete o esquema, lembrando que cada dose deve ter um intervalo de 30 dias
	- *Hepatite B*: Se não tiver sido imunizada (Olhar Cartão ou pedir Anti-Hbs (se não reagente vacinar))
		- 3 doses: 0, 30 e 180 dias
		- Se HIV +: Dose dobrada + 4 doses (0, 1, 2 e 6 ou 12m)
	- *COVID-19*: Em qualquer idade gestacional, aplicar se última dose há mais de 6m. vacinas liberadas (Corona, Pfizer ou Moderna)
	- *Vírus Sincial Respiratório (VSR)*: 32-36 semanas (intervalo de ao menos 14d entre a vacina e o parto)
		- Indicada para toda gestante em toda gestação
- **Vacinas Contraindicadas na Gestação** (as de vírus vivo atenuado): Sarampo, caxumba e rubéola (SCR), Poliomielite (VOP), varicela e Dengue
- **Vacinas em Casos Especiais**
	- *Surtos ou regiões endêmicas*: Hepatite A, Febre Amarela e Menigocócica
	- *Pneumocócica*: Apenas se gestante for: cardiopata, asplênica, pneumopata ou imunodeprimida
	- *Raiva*: Se houver exposição
## 🩸 Rastreio de Exames Pré-Natais

### 🔹 1º Trimestre
- [ ] **Tipagem Sanguínea + Fator Rh**: Se Rh negativo → Coombs Indireto mensal. Ver [[Doença Hemolítica Perinatal]]
- [ ] **Hemograma Completo**
- [ ] **Glicemia de Jejum**: Se alterado → Ver [[Diabetes Mellitus na Gestação]]
- [ ] **EAS + Urocultura**
- [ ] **HIV**
- [ ] **Sífilis**
- [ ] **Toxoplasmose IgM e IgG**: Acompanhamento mensal/trimestral
- [ ] **Hepatite B e C**
- [ ] **HTLV**
---
### 🔹 2º Trimestre (24 a 28 semanas)
- [ ] **TOTG 75g**: Apenas se Glicemia de Jejum do 1º trimestre estiver normal
- [ ] **Toxoplasmose IgM e IgG**: Manter rastreio periódico
---
### 🔹 3º Trimestre (>28 semanas)
- [ ] **Hemograma Completo**
- [ ] **EAS + Urocultura**
- [ ] **HIV** (Repetir no 3º trimestre/parto)
- [ ] **Sífilis** (Repetir no 3º trimestre/parto)
- [ ] **Hepatite B e C** (Repetir no 3º trimestre se exposição)
- [ ] **Toxoplasmose IgM e IgG**: Manter rastreio periódico
- [ ] **Cultura para Streptococcus do grupo B (Swab vaginal e anal)**: Realizar de 36 semanas a 37 semanas e 6 dias

| **Locais Para achar o BCF**               |
| ----------------------------------------- |
| ![[Pasted image 20261025141806.png\|308]] |


```dataviewjs
const container = dv.container;
container.innerHTML = "";

const htmlContent = `
<div style="background: var(--background-secondary); padding: 20px; border-radius: 12px; border: 1px solid var(--background-modifier-border); font-family: var(--default-font); max-width: 500px; box-shadow: 0 4px 12px rgba(0,0,0,0.05);">
    <h3 style="margin-top: 0; margin-bottom: 16px; color: var(--text-normal); font-size: 1.1em; display: flex; align-items: center; gap: 8px;">
        👶 Calculadora Gestacional
    </h3>
    
    <div style="display: flex; gap: 20px; margin-bottom: 16px; font-size: 0.95em;">
        <label style="cursor: pointer; display: flex; align-items: center; gap: 6px;">
            <input type="radio" name="dv_metodo_calc" value="dum" checked style="cursor: pointer;"> Por DUM
        </label>
        <label style="cursor: pointer; display: flex; align-items: center; gap: 6px;">
            <input type="radio" name="dv_metodo_calc" value="usg" style="cursor: pointer;"> Por USG
        </label>
    </div>

    <!-- Seção DUM -->
    <div id="box_dum" style="margin-bottom: 14px;">
        <label style="font-size: 0.85em; color: var(--text-muted); display: block; margin-bottom: 4px;">Data da Última Menstruação (DUM):</label>
        <input type="date" id="input_val_dum" style="width: 100%; padding: 8px; border-radius: 6px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-normal); box-sizing: border-box;">
    </div>

    <!-- Seção USG -->
    <div id="box_usg" style="display: none; margin-bottom: 14px;">
        <label style="font-size: 0.85em; color: var(--text-muted); display: block; margin-bottom: 4px;">Data da Realização do USG:</label>
        <input type="date" id="input_val_usg" style="width: 100%; padding: 8px; margin-bottom: 10px; border-radius: 6px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-normal); box-sizing: border-box;">
        
        <label style="font-size: 0.85em; color: var(--text-muted); display: block; margin-bottom: 4px;">Idade Gestacional na data do USG:</label>
        <div style="display: flex; gap: 8px;">
            <div style="flex: 1;">
                <input type="number" id="input_usg_sem" placeholder="Semanas" min="0" max="42" style="width: 100%; padding: 8px; border-radius: 6px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-normal); box-sizing: border-box;">
            </div>
            <span style="display: flex; align-items: center; color: var(--text-muted); font-size: 0.9em;">sem e</span>
            <div style="flex: 1;">
                <input type="number" id="input_usg_dias" placeholder="Dias (0-6)" min="0" max="6" style="width: 100%; padding: 8px; border-radius: 6px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-normal); box-sizing: border-box;">
            </div>
        </div>
    </div>

    <button id="btn_exec_calc" style="width: 100%; padding: 10px; border-radius: 6px; background: var(--interactive-accent); color: var(--text-on-accent); border: none; cursor: pointer; font-weight: 500; transition: opacity 0.2s;">Calcular</button>

    <!-- Resultado -->
    <div id="res_container" style="margin-top: 18px; display: none; padding-top: 14px; border-top: 1px dashed var(--background-modifier-border);"></div>
</div>
`;

container.innerHTML = htmlContent;

const radios = container.querySelectorAll('input[name="dv_metodo_calc"]');
const boxDum = container.querySelector('#box_dum');
const boxUsg = container.querySelector('#box_usg');
const btnCalc = container.querySelector('#btn_exec_calc');
const resContainer = container.querySelector('#res_container');

radios.forEach(radio => {
    radio.addEventListener('change', (e) => {
        if (e.target.value === 'dum') {
            boxDum.style.display = 'block';
            boxUsg.style.display = 'none';
        } else {
            boxDum.style.display = 'none';
            boxUsg.style.display = 'block';
        }
    });
});

btnCalc.addEventListener('click', () => {
    const metodo = container.querySelector('input[name="dv_metodo_calc"]:checked').value;
    const hoje = moment();
    let dpp, margemErro, igDias, dumTeorica;

    if (metodo === 'dum') {
        const valDum = container.querySelector('#input_val_dum').value;
        if (!valDum) {
            new Notice("Por favor, selecione a data da DUM.");
            return;
        }
        dumTeorica = moment(valDum);
        dpp = dumTeorica.clone().add(280, 'days');
        igDias = hoje.diff(dumTeorica, 'days');
        margemErro = "± 14 dias (2 semanas)";
    } else {
        const valUsg = container.querySelector('#input_val_usg').value;
        const sem = parseInt(container.querySelector('#input_usg_sem').value) || 0;
        const dias = parseInt(container.querySelector('#input_usg_dias').value) || 0;

        if (!valUsg) {
            new Notice("Por favor, selecione a data do USG.");
            return;
        }

        const dataUsg = moment(valUsg);
        const totalDiasUsg = (sem * 7) + dias;
        
        dumTeorica = dataUsg.clone().subtract(totalDiasUsg, 'days');
        dpp = dumTeorica.clone().add(280, 'days');
        igDias = hoje.diff(dumTeorica, 'days');

        if (sem < 14) {
            margemErro = "± 5 a 7 dias (USG 1º Trimestre)";
        } else if (sem < 28) {
            margemErro = "± 10 a 14 dias (USG 2º Trimestre)";
        } else {
            margemErro = "± 21 dias / 3 semanas (USG 3º Trimestre)";
        }
    }

    const semanasAtual = Math.floor(igDias / 7);
    const diasAtual = igDias % 7;

    resContainer.style.display = "block";
    resContainer.innerHTML = `
        <div style="font-size: 0.95em; line-height: 1.6;">
            <div style="margin-bottom: 6px;"><strong>Idade Gestacional Hoje:</strong> <span style="color: var(--interactive-accent); font-weight: 600;">${semanasAtual} semanas e ${diasAtual} dias</span></div>
            <div style="margin-bottom: 6px;"><strong>Data Provável do Parto (DPP):</strong> <span style="color: var(--text-normal); font-weight: 600;">${dpp.format('DD/MM/YYYY')}</span></div>
            <div style="margin-bottom: 6px; font-size: 0.85em; color: var(--text-muted);"><strong>Margem de Erro da DPP:</strong> ${margemErro}</div>
            <div style="font-size: 0.85em; color: var(--text-muted);"><strong>DUM (ou DUM Teórica):</strong> ${dumTeorica.format('DD/MM/YYYY')}</div>
        </div>
    `;
});
```

```dataviewjs
const container = dv.container;
container.innerHTML = "";

const htmlContent = `
<div style="background: var(--background-secondary); padding: 20px; border-radius: 12px; border: 1px solid var(--background-modifier-border); font-family: var(--default-font); max-width: 520px; box-shadow: 0 4px 12px rgba(0,0,0,0.05);">
    <h3 style="margin-top: 0; margin-bottom: 16px; color: var(--text-normal); font-size: 1.1em; display: flex; align-items: center; gap: 8px;">
        ⚖️ Avaliação de Ganho de Peso Gestacional
    </h3>
    
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 12px;">
        <div>
            <label style="font-size: 0.85em; color: var(--text-muted); display: block; margin-bottom: 4px;">Peso Pré-Gravídico (kg):</label>
            <input type="number" id="peso_pre" step="0.1" placeholder="Ex: 60.5" style="width: 100%; padding: 8px; border-radius: 6px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-normal); box-sizing: border-box;">
        </div>
        <div>
            <label style="font-size: 0.85em; color: var(--text-muted); display: block; margin-bottom: 4px;">Altura (m):</label>
            <input type="number" id="altura" step="0.01" placeholder="Ex: 1.65" style="width: 100%; padding: 8px; border-radius: 6px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-normal); box-sizing: border-box;">
        </div>
    </div>

    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 16px;">
        <div>
            <label style="font-size: 0.85em; color: var(--text-muted); display: block; margin-bottom: 4px;">Peso Atual (kg):</label>
            <input type="number" id="peso_atual" step="0.1" placeholder="Ex: 68.0" style="width: 100%; padding: 8px; border-radius: 6px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-normal); box-sizing: border-box;">
        </div>
        <div>
            <label style="font-size: 0.85em; color: var(--text-muted); display: block; margin-bottom: 4px;">Idade Gestacional (Semanas):</label>
            <input type="number" id="ig_atual" placeholder="Ex: 24" style="width: 100%; padding: 8px; border-radius: 6px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-normal); box-sizing: border-box;">
        </div>
    </div>

    <button id="btn_calc_peso" style="width: 100%; padding: 10px; border-radius: 6px; background: var(--interactive-accent); color: var(--text-on-accent); border: none; cursor: pointer; font-weight: 500;">Avaliar Ganho de Peso</button>

    <!-- Resultado -->
    <div id="res_peso_container" style="margin-top: 18px; display: none; padding-top: 14px; border-top: 1px dashed var(--background-modifier-border);"></div>
</div>
`;

container.innerHTML = htmlContent;

const btnCalc = container.querySelector('#btn_calc_peso');
const resContainer = container.querySelector('#res_peso_container');

btnCalc.addEventListener('click', () => {
    const pPre = parseFloat(container.querySelector('#peso_pre').value);
    const alt = parseFloat(container.querySelector('#altura').value);
    const pAtual = parseFloat(container.querySelector('#peso_atual').value);
    const ig = parseInt(container.querySelector('#ig_atual').value);

    if (!pPre || !alt || !pAtual || isNaN(ig)) {
        new Notice("Por favor, preencha todos os campos corretamente.");
        return;
    }

    const imcPre = pPre / (alt * alt);
    let classificacao = "";
    let minGanhoTotal = 0;
    let maxGanhoTotal = 0;

    if (imcPre < 19.8) {
        classificacao = "Baixo Peso";
        minGanhoTotal = 12.5;
        maxGanhoTotal = 18.0;
    } else if (imcPre >= 19.8 && imcPre <= 26.0) {
        classificacao = "Normal";
        minGanhoTotal = 11.5;
        maxGanhoTotal = 16.0;
    } else if (imcPre > 26.0 && imcPre <= 29.0) {
        classificacao = "Sobrepeso";
        minGanhoTotal = 7.0;
        maxGanhoTotal = 11.5;
    } else {
        classificacao = "Obesidade";
        minGanhoTotal = 0;
        maxGanhoTotal = 7.0;
    }

    const ganhoAtual = pAtual - pPre;
    let statusGanho = "Adequado / Em acompanhamento";
    
    if (ig > 0 && ig <= 40) {
        const proporcao = ig / 40;
        const ganhoEsperadoMin = minGanhoTotal * proporcao;
        const ganhoEsperadoMax = maxGanhoTotal * proporcao;
        
        if (ganhoAtual < ganhoEsperadoMin - 1.0) {
            statusGanho = "⚠️ Ganho abaixo do esperado para a IG";
        } else if (ganhoAtual > ganhoEsperadoMax + 1.0) {
            statusGanho = "⚠️ Ganho acima do esperado para a IG";
        } else {
            statusGanho = "✅ Ganho de peso adequado para a IG";
        }
    }

    resContainer.style.display = "block";
    resContainer.innerHTML = `
        <div style="font-size: 0.95em; line-height: 1.6;">
            <div style="margin-bottom: 6px;"><strong>IMC Pré-gravídico:</strong> <span style="color: var(--text-normal); font-weight: 600;">${imcPre.toFixed(2)} kg/m²</span> (${classificacao})</div>
            <div style="margin-bottom: 6px;"><strong>Ganho Total Recomendado:</strong> <span style="color: var(--interactive-accent); font-weight: 600;">${imcPre > 29.0 ? 'Até 7.0 kg' : minGanhoTotal + ' a ' + maxGanhoTotal + ' kg'}</span></div>
            <div style="margin-bottom: 6px;"><strong>Ganho Atual (${ig} semanas):</strong> <span style="color: var(--text-normal); font-weight: 600;">${ganhoAtual >= 0 ? '+' : ''}${ganhoAtual.toFixed(1)} kg</span></div>
            <div style="margin-top: 10px; padding: 8px; background: var(--background-primary); border-radius: 6px; font-weight: 500; text-align: center;">${statusGanho}</div>
        </div>
    `;
});
```


```dataviewjs
const root = dv.container;
root.innerHTML = "";

const box = document.createElement("div");
box.style.cssText = `
  border: 1px solid var(--background-modifier-border);
  border-radius: 12px;
  padding: 16px;
  max-width: 600px;
`;

box.innerHTML = `
  <h3 style="margin-top:0">🤰 Calculadora de ganho ponderal — Pré-natal</h3>

  <p style="margin-bottom:6px"><b>Consulta anterior</b></p>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px">
    <label>
      Peso (kg)
      <input id="peso1" type="number" min="0" step="0.01"
        placeholder="Ex.: 68,5"
        style="width:100%;box-sizing:border-box">
    </label>
    <label>
      Data
      <input id="data1" type="date"
        style="width:100%;box-sizing:border-box">
    </label>
  </div>

  <p style="margin:16px 0 6px"><b>Consulta atual</b></p>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px">
    <label>
      Peso (kg)
      <input id="peso2" type="number" min="0" step="0.01"
        placeholder="Ex.: 70,2"
        style="width:100%;box-sizing:border-box">
    </label>
    <label>
      Data
      <input id="data2" type="date"
        style="width:100%;box-sizing:border-box">
    </label>
  </div>

  <button id="calcular" style="
    margin-top:16px;padding:10px 16px;width:100%;
    border:0;border-radius:8px;cursor:pointer;
    background:var(--interactive-accent);color:white;font-weight:bold">
    Calcular ganho ponderal
  </button>

  <div id="resultado" aria-live="polite" style="margin-top:16px"></div>
`;

root.appendChild(box);

const el = id => box.querySelector("#" + id);

function numero(id) {
  const valor = el(id).value.trim().replace(",", ".");
  return valor === "" ? NaN : Number(valor);
}

el("calcular").addEventListener("click", () => {
  const p1 = numero("peso1");
  const p2 = numero("peso2");
  const d1 = el("data1").value;
  const d2 = el("data2").value;
  const out = el("resultado");

  if (!Number.isFinite(p1) || !Number.isFinite(p2) ||
      p1 <= 0 || p2 <= 0 || !d1 || !d2) {
    out.innerHTML = "<p>Preencha os dois pesos e as duas datas.</p>";
    return;
  }

  const inicio = new Date(d1 + "T12:00:00Z");
  const fim = new Date(d2 + "T12:00:00Z");
  const dias = Math.round((fim - inicio) / 86400000);

  if (dias <= 0) {
    out.innerHTML = "<p>A data da consulta atual deve ser posterior à anterior.</p>";
    return;
  }

  const ganho = p2 - p1;
  const semanal = ganho / dias * 7;
  const diario = ganho * 1000 / dias;

  const fmt = (n, casas = 2) =>
    n.toLocaleString("pt-BR", {
      minimumFractionDigits: casas,
      maximumFractionDigits: casas
    });

  const sinal = n => n > 0 ? "+" : "";

  let descricao;
  if (ganho > 0) descricao = "Ganho de peso";
  else if (ganho < 0) descricao = "Perda de peso";
  else descricao = "Peso estável";

  out.innerHTML = `
    <div style="
      background:var(--background-secondary);
      border-radius:10px;padding:14px">
      <p style="margin-top:0;font-weight:bold">${descricao}</p>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:14px">
        <div>
          <small>Variação de peso</small>
          <div style="font-size:1.4em;font-weight:bold">
            ${sinal(ganho)}${fmt(ganho)} kg
          </div>
        </div>
        <div>
          <small>Intervalo</small>
          <div style="font-size:1.4em;font-weight:bold">
            ${dias} dias
          </div>
        </div>
        <div>
          <small>Variação semanal</small>
          <div style="font-size:1.2em;font-weight:bold">
            ${sinal(semanal)}${fmt(semanal)} kg/semana
          </div>
        </div>
        <div>
          <small>Variação diária</small>
          <div style="font-size:1.2em;font-weight:bold">
            ${sinal(diario)}${fmt(diario, 1)} g/dia
          </div>
        </div>
      </div>
      <hr>
      <small>
        Peso anterior: ${fmt(p1)} kg ·
        Peso atual: ${fmt(p2)} kg
      </small>
    </div>
    <p style="font-size:0.85em;color:var(--text-muted)">
      Resultado descritivo. A adequação do ganho deve considerar
      IMC pré-gestacional, idade gestacional, gestação única ou múltipla
      e evolução clínica.
    </p>
  `;
});
```


```dataviewjs
const container = dv.container;
container.innerHTML = "";

const htmlContent = `
<div style="background: var(--background-secondary); padding: 20px; border-radius: 12px; border: 1px solid var(--background-modifier-border); font-family: var(--default-font); max-width: 540px; box-shadow: 0 4px 12px rgba(0,0,0,0.05);">
    <h3 style="margin-top: 0; margin-bottom: 16px; color: var(--text-normal); font-size: 1.1em; display: flex; align-items: center; gap: 8px;">
        📏 Avaliação Gráfica da Altura Uterina
    </h3>
    
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 16px;">
        <div>
            <label style="font-size: 0.85em; color: var(--text-muted); display: block; margin-bottom: 4px;">Idade Gestacional (Semanas):</label>
            <input type="number" id="au_ig" placeholder="Ex: 20" min="10" max="42" style="width: 100%; padding: 8px; border-radius: 6px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-normal); box-sizing: border-box;">
        </div>
        <div>
            <label style="font-size: 0.85em; color: var(--text-muted); display: block; margin-bottom: 4px;">Medida Atual (cm):</label>
            <input type="number" id="au_cm" step="0.5" placeholder="Ex: 20.0" style="width: 100%; padding: 8px; border-radius: 6px; border: 1px solid var(--background-modifier-border); background: var(--background-primary); color: var(--text-normal); box-sizing: border-box;">
        </div>
    </div>

    <button id="btn_calc_au" style="width: 100%; padding: 10px; border-radius: 6px; background: var(--interactive-accent); color: var(--text-on-accent); border: none; cursor: pointer; font-weight: 500;">Gerar Avaliação e Gráfico</button>

    <!-- Área Gráfica e Resultados -->
    <div id="res_au_container" style="margin-top: 18px; display: none; padding-top: 14px; border-top: 1px dashed var(--background-modifier-border);">
        <div style="display: flex; flex-direction: column; align-items: center; margin-bottom: 15px;">
            <div style="font-size: 0.85em; color: var(--text-muted); margin-bottom: 8px; font-weight: 500;">Esquema Gráfico do Fundo Uterino</div>
            
            <!-- Contenedor do Desenho da Barriga -->
            <div style="position: relative; width: 160px; height: 240px; background: var(--background-primary); border: 2px solid var(--background-modifier-border); border-radius: 80px 80px 40px 40px; display: flex; justify-content: center; align-items: flex-end; overflow: hidden; box-shadow: inset 0 0 10px rgba(0,0,0,0.05);">
                
                <!-- Referência de Sínfise Púbica (Base) -->
                <div style="position: absolute; bottom: 5px; font-size: 9px; color: var(--text-muted); z-index: 3;">Sínfise Púbica</div>
                
                <!-- Referência Cicatriz Umbilical (Meio) -->
                <div style="position: absolute; top: 115px; display: flex; align-items: center; gap: 4px; z-index: 3;">
                    <div style="width: 6px; height: 6px; background: #e06c75; border-radius: 50%;"></div>
                    <span style="font-size: 9px; color: var(--text-muted);">Umbigo (20s)</span>
                </div>

                <!-- Curva/Útero Gráfico Dinâmico -->
                <div id="grafico_utero" style="position: absolute; bottom: 10px; width: 100px; background: rgba(86, 182, 194, 0.25); border: 2px dashed var(--interactive-accent); border-radius: 50px 50px 20px 20px; transition: height 0.4s ease; z-index: 2; display: flex; justify-content: center; align-items: flex-start; padding-top: 5px;">
                    <span id="label_altura_grafico" style="font-size: 10px; font-weight: bold; color: var(--text-normal);"></span>
                </div>
            </div>
        </div>

        <div id="texto_resultado_au" style="font-size: 0.95em; line-height: 1.6;"></div>
    </div>
</div>
`;

container.innerHTML = htmlContent;

const btnCalc = container.querySelector('#btn_calc_au');
const resContainer = container.querySelector('#res_au_container');
const uteroGrafico = container.querySelector('#grafico_utero');
const labelGrafico = container.querySelector('#label_altura_grafico');
const textoResultado = container.querySelector('#texto_resultado_au');

btnCalc.addEventListener('click', () => {
    const ig = parseInt(container.querySelector('#au_ig').value);
    const medidaCm = parseFloat(container.querySelector('#au_cm').value);

    if (isNaN(ig) || ig < 10 || ig > 42) {
        new Notice("Por favor, insira uma idade gestacional válida entre 10 e 42 semanas.");
        return;
    }

    let referenciaAnatomica = "";
    let esperadoMin = 0;
    let esperadoMax = 0;

    if (ig === 12) {
        referenciaAnatomica = "Sínfise púbica";
        esperadoMin = 10; esperadoMax = 14;
    } else if (ig === 16) {
        referenciaAnatomica = "Entre a sínfise púbica e a cicatriz umbilical";
        esperadoMin = 14; esperadoMax = 18;
    } else if (ig === 20) {
        referenciaAnatomica = "Cicatriz umbilical";
        esperadoMin = 18; esperadoMax = 22;
    } else if (ig > 20 && ig <= 32) {
        referenciaAnatomica = "Crescimento de cerca de 1 cm por semana";
        esperadoMin = ig - 2;
        esperadoMax = ig + 2;
    } else if (ig > 32) {
        referenciaAnatomica = "Ritmo de crescimento de cerca de 0,5 cm por semana";
        esperadoMin = ig - 3;
        esperadoMax = ig + 3;
    } else {
        referenciaAnatomica = "Abaixo de 12 semanas (útero intrapélvico)";
        esperadoMin = 0; esperadoMax = 5;
    }

    let statusMedida = "Sem medida informada";
    if (!isNaN(medidaCm)) {
        if (medidaCm < esperadoMin) {
            statusMedida = "⚠️ Altura uterina abaixo do esperado para a IG";
        } else if (medidaCm > esperadoMax) {
            statusMedida = "⚠️ Altura uterina acima do esperado para a IG";
        } else {
            statusMedida = "✅ Altura uterina compatível com a IG";
        }
    }

    // Cálculo proporcional da altura visual do útero no gráfico (escala de 10cm a 40cm mapeada para 20px a 200px de altura)
    let alturaPixels = 30;
    if (!isNaN(medidaCm)) {
        alturaPixels = Math.min(Math.max((medidaCm / 40) * 200, 25), 210);
    } else {
        // Baseado na IG caso não tenha medida em cm
        let cmEstimado = ig <= 12 ? 12 : (ig === 16 ? 16 : (ig === 20 ? 20 : ig));
        alturaPixels = Math.min(Math.max((cmEstimado / 40) * 200, 25), 210);
    }

    uteroGrafico.style.height = alturaPixels + "px";
    labelGrafico.innerText = !isNaN(medidaCm) ? medidaCm + " cm" : ig + " sem";

    resContainer.style.display = "block";
    textoResultado.innerHTML = `
        <div style="margin-bottom: 6px;"><strong>Referência Anatômica (${ig} sem):</strong> <span style="color: var(--text-normal); font-weight: 600;">${referenciaAnatomica}</span></div>
        ${!isNaN(medidaCm) ? `
            <div style="margin-bottom: 6px;"><strong>Medida Informada:</strong> <span style="color: var(--interactive-accent); font-weight: 600;">${medidaCm} cm</span> (Esperado aprox.: ${esperadoMin} a${esperadoMax} cm)</div>
            <div style="margin-top: 10px; padding: 8px; background: var(--background-primary); border-radius: 6px; font-weight: 500; text-align: center;">${statusMedida}</div>
        ` : '<div style="font-size: 0.85em; color: var(--text-muted); margin-top: 6px;">Dica: Preencha a medida em cm para ajustar o gráfico com precisão.</div>'}
    `;
});
```

```dataviewjs
const container = dv.container;
container.innerHTML = "";

const htmlContent = `
<style>
  @keyframes animLeopold {
    0%, 22% { /* 1ª Manobra */
        --pos-mao-top: 15px;
        --pos-mao-left: 25px;
        --pos-mao-right: 25px;
        --pos-feto-top: 25px;
        --feto-altura: 130px;
        --feto-largura: 60px;
        --rotacao-mao: 0deg;
    }
    28%, 48% { /* 2ª Manobra */
        --pos-mao-top: 90px;
        --pos-mao-left: 5px;
        --pos-mao-right: 5px;
        --pos-feto-top: 20px;
        --feto-altura: 140px;
        --feto-largura: 65px;
        --rotacao-mao: 0deg;
    }
    54%, 74% { /* 3ª Manobra */
        --pos-mao-top: 175px;
        --pos-mao-left: 70px;
        --pos-mao-right: 70px;
        --pos-feto-top: 15px;
        --feto-altura: 130px;
        --feto-largura: 60px;
        --rotacao-mao: 90deg;
    }
    80%, 100% { /* 4ª Manobra */
        --pos-mao-top: 195px;
        --pos-mao-left: 30px;
        --pos-mao-right: 30px;
        --pos-feto-top: 30px;
        --feto-altura: 120px;
        --feto-largura: 55px;
        --rotacao-mao: 45deg;
    }
  }

  .container-animado {
    animation: animLeopold 14s infinite ease-in-out;
  }
  
  /* Sincronização dos textos e indicadores visuais com o tempo da animação */
  @keyframes mudarTexto {
    0%, 22% { content: "1ª Manobra: Fundo Uterino (Delimitação do polo superior)"; opacity: 1; }
    23%, 27% { opacity: 0; }
    28%, 48% { content: "2ª Manobra: Laterais (Identificação do dorso fetal)"; opacity: 1; }
    49%, 53% { opacity: 0; }
    54%, 74% { content: "3ª Manobra: Pólo Inferior (Verificação da apresentação)"; opacity: 1; }
    75%, 79% { opacity: 0; }
    80%, 100% { content: "4ª Manobra: Pelve (Grau de insinuação/encaixe)"; opacity: 1; }
  }

  .texto-dinamico {
    animation: mudarTexto 14s infinite;
  }
</style>

<div style="background: var(--background-secondary); padding: 24px; border-radius: 16px; border: 1px solid var(--background-modifier-border); font-family: var(--default-font); max-width: 520px; box-shadow: 0 8px 24px rgba(0,0,0,0.08); text-align: center; margin: 0 auto;">
    
    <h3 style="margin-top: 0; margin-bottom: 12px; color: var(--text-normal); font-size: 1.15em;">
        🔄 Animação Contínua: Manobras de Leopold
    </h3>

    <!-- Caixa de Legenda Animada em tempo real -->
    <div style="background: var(--background-primary); padding: 12px; border-radius: 8px; border: 1px solid var(--background-modifier-border); margin-bottom: 16px; min-height: 45px; display: flex; align-items: center; justify-content: center;">
        <span class="texto-dinamico" style="font-weight: 600; color: var(--interactive-accent); font-size: 0.95em;"></span>
    </div>

    <!-- Palco Gráfico da Animação -->
    <div class="container-animado" style="position: relative; width: 200px; height: 280px; margin: 0 auto; background: var(--background-primary); border: 3px solid var(--background-modifier-border); border-radius: 100px 100px 50px 50px; overflow: hidden; box-shadow: inset 0 0 15px rgba(0,0,0,0.08);">
        
        <!-- Referências anatômicas fixas -->
        <div style="position: absolute; bottom: 6px; width: 100%; font-size: 8px; color: var(--text-muted); text-transform: uppercase; letter-spacing: 1px; z-index: 5;">Sínfise Púbica</div>
        <div style="position: absolute; top: 115px; left: 50%; transform: translateX(-50%); display: flex; align-items: center; gap: 3px; z-index: 5;">
            <div style="width: 6px; height: 6px; background: #e06c75; border-radius: 50%;"></div>
            <span style="font-size: 8px; color: var(--text-muted);">Umbigo</span>
        </div>

        <!-- Útero Fundo -->
        <div style="position: absolute; bottom: 10px; left: 50%; transform: translateX(-50%); width: 140px; height: 230px; background: rgba(86, 182, 194, 0.15); border: 2px dashed rgba(86, 182, 194, 0.5); border-radius: 70px 70px 25px 25px; z-index: 1;"></div>

        <!-- Feto Animado -->
        <div style="position: absolute; left: 50%; transform: translateX(-50%); top: var(--pos-feto-top, 25px); width: var(--feto-largura, 60px); height: var(--feto-altura, 130px); background: linear-gradient(135deg, rgba(152, 195, 121, 0.4), rgba(86, 182, 194, 0.4)); border: 2px solid #98c379; border-radius: 30px; z-index: 2; transition: all 0.5s ease-in-out;">
            <div style="width: 25px; height: 25px; background: #98c379; border-radius: 50%; margin: 4px auto; opacity: 0.8;"></div>
        </div>

        <!-- Mão Esquerda Animada -->
        <div style="position: absolute; top: var(--pos-mao-top, 15px); left: var(--pos-mao-left, 25px); width: 40px; height: 22px; background: var(--text-normal); border-radius: 10px; opacity: 0.85; z-index: 4; transition: all 0.5s ease-in-out; transform: rotate(var(--rotacao-mao, 0deg)); box-shadow: 0 2px 6px rgba(0,0,0,0.2);"></div>

        <!-- Mão Direita Animada -->
        <div style="position: absolute; top: var(--pos-mao-top, 15px); right: var(--pos-mao-right, 25px); width: 40px; height: 22px; background: var(--text-normal); border-radius: 10px; opacity: 0.85; z-index: 4; transition: all 0.5s ease-in-out; transform: rotate(calc(var(--rotacao-mao, 0deg) * -1)); box-shadow: 0 2px 6px rgba(0,0,0,0.2);"></div>

    </div>
    
    <div style="margin-top: 14px; font-size: 0.8em; color: var(--text-muted);">
        A animação roda de forma contínua e cíclica automaticamente.
    </div>
</div>
`;
```
