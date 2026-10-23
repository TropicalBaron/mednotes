
# 👶 Prontuário Pediátrico Integrado com Puericultura, DNPM & Vacinação

```dataviewjs
dv.container.innerHTML = "";

const wrapper = document.createElement("div");
wrapper.id = "pueri-full-app";

const style = document.createElement("style");
style.textContent = 
  "#pueri-full-app { font-family: var(--font-text); }" +
  "#pueri-full-app .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(145px, 1fr)); gap: 10px; }" +
  "#pueri-full-app .grid-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 10px; }" +
  "#pueri-full-app label { display: block; font-size: .85em; margin-bottom: 4px; font-weight: 600; }" +
  "#pueri-full-app input[type='text'], #pueri-full-app input[type='number'], #pueri-full-app input[type='date'], #pueri-full-app select, #pueri-full-app textarea { width: 100%; height: 38px; padding: 6px 10px; border: 1px solid var(--background-modifier-border); border-radius: 6px; background: var(--background-primary); color: var(--text-normal); box-sizing: border-box; }" +
  "#pueri-full-app button { margin: 15px 5px 15px 0; padding: 10px 18px; border: 1px solid var(--background-modifier-border); border-radius: 6px; cursor: pointer; font-weight: bold; background: var(--interactive-accent); color: var(--text-on-accent); }" +
  "#pueri-full-app .resultado { padding: 14px; background: var(--background-secondary); border-radius: 8px; margin: 12px 0; line-height: 1.6; }" +
  "#pueri-full-app fieldset { border: 1px solid var(--background-modifier-border); border-radius: 6px; padding: 12px; margin: 12px 0; }" +
  "#pueri-full-app legend { font-size: .85em; font-weight: bold; padding: 0 6px; }" +
  "#pueri-full-app table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 0.88em; }" +
  "#pueri-full-app th, #pueri-full-app td { border: 1px solid var(--background-modifier-border); padding: 8px; text-align: left; }" +
  "#pueri-full-app th { background: var(--background-secondary-alt); }" +
  "#pueri-full-app .charts-grid { display: grid; grid-template-columns: 1fr; gap: 25px; margin-top: 15px; }" +
  "#pueri-full-app .chart-card { background: var(--background-primary); border: 1px solid var(--background-modifier-border); border-radius: 8px; padding: 14px; text-align: center; box-shadow: 0 2px 4px rgba(0,0,0,0.05); position: relative; }" +
  "#pueri-full-app .chart-card.disabled { opacity: 0.4; filter: grayscale(100%); background: var(--background-secondary-alt); }" +
  "#pueri-full-app .chart-title { font-weight: bold; font-size: 1em; margin-bottom: 6px; text-align: left; color: var(--text-normal); }" +
  "#pueri-full-app .chart-badge { font-size: 0.75em; padding: 2px 6px; border-radius: 4px; background: var(--background-secondary-alt); border: 1px solid var(--background-modifier-border); display: inline-block; margin-bottom: 8px; float: right; }" +
  "#pueri-full-app svg { width: 100%; height: auto; max-height: 300px; overflow: visible; }" +
  "#pueri-full-app .na-overlay { position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); background: rgba(0,0,0,0.75); color: #fff; padding: 8px 16px; border-radius: 6px; font-weight: bold; font-size: 0.9em; pointer-events: none; }" +
  "#pueri-full-app details { margin-bottom: 12px; border: 1px solid var(--background-modifier-border); border-radius: 6px; padding: 8px 12px; background: var(--background-primary); }" +
  "#pueri-full-app summary { font-weight: bold; cursor: pointer; padding: 4px 0; outline: none; }" +
  "#pueri-full-app details[open] { background: var(--background-primary-alt); }" +
  "#pueri-full-app .checkbox-item { display: flex; align-items: center; font-size: 0.9em; }" +
  "#pueri-full-app .checkbox-item input[type='checkbox'] { width: 18px; height: 18px; margin-right: 6px; cursor: pointer; }" +
  "#pueri-full-app .badge-dnpm { font-size: 0.75em; padding: 2px 6px; border-radius: 4px; font-weight: bold; margin-left: 8px; }" +
  "#pueri-full-app .badge-alerta { background: #e74c3c; color: #fff; }" +
  "#pueri-full-app .relatorio-box { background: var(--background-secondary-alt); border: 1px dashed var(--interactive-accent); padding: 15px; border-radius: 8px; font-family: monospace; white-space: pre-wrap; font-size: 0.9em; max-height: 400px; overflow-y: auto; }" +
  "#pueri-full-app .alerta-vacina { background: var(--background-secondary); border-left: 4px solid #f39c12; padding: 10px; font-size: 0.85em; margin-bottom: 15px; border-radius: 4px; }";

wrapper.appendChild(style);

const bodyDiv = document.createElement("div");
bodyDiv.innerHTML = [
  '<h3>1. Identificação do Paciente</h3>',
  '<div class="grid">',
    '<div style="grid-column: span 2;"><label>Nome do Paciente</label><input id="nome_paciente" type="text" placeholder="Nome completo da criança"></div>',
    '<div><label>Sexo</label><select id="sexo"><option value="M">Masculino</option><option value="F">Feminino</option></select></div>',
    '<div><label>Data da consulta atual</label><input id="data" type="date"></div>',
    '<div><label>Data de nascimento</label><input id="nasc" type="date"></div>',
    '<div><label>Data da última consulta</label><input id="data_ant" type="date"></div>',
    '<div><label>IG ao nascer (semanas)</label><input id="ig" type="number" min="24" max="43" value="40" step="1"></div>',
  '</div>',

  '<h3 style="margin-top:20px;">2. Medidas Antropométricas & Ganho Ponderal</h3>',
  '<div class="grid">',
    '<div><label>Peso atual (kg)</label><input id="peso" type="number" min="0" step=".001"></div>',
    '<div><label>Comprimento/Estatura (cm)</label><input id="est" type="number" min="0" step=".1"></div>',
    '<div><label>Perímetro Cefálico (cm)</label><input id="pc" type="number" min="0" step=".1"></div>',
    '<div><label>Perímetro Abdominal (cm)</label><input id="pa" type="number" min="0" step=".1"></div>',
    '<div><label>Perímetro Torácico (cm)</label><input id="pt" type="number" min="0" step=".1"></div>',
  '</div>',

  '<fieldset style="margin-top:10px;">',
    '<legend>Fontanelas</legend>',
    '<div class="grid">',
      '<div><label>Fontanela Anterior</label><select id="fa_status"><option value="Aberta">Aberta</option><option value="Normotensa">Normotensa</option><option value="Deprimida">Deprimida</option><option value="Abaulada">Abaulada</option><option value="Fechada">Fechada</option></select></div>',
      '<div><label>Medida Anterior</label><input id="fa_val" type="number" min="0" step="0.1" placeholder="Ex: 2"></div>',
      '<div><label>Unidade Anterior</label><select id="fa_unid"><option value="cm">cm</option><option value="polpa(s) digital(ais)">polpa(s) digital(ais)</option></select></div>',
    '</div>',
    '<div class="grid" style="margin-top:10px;">',
      '<div><label>Fontanela Posterior</label><select id="fp_status"><option value="Fechada">Fechada</option><option value="Aberta">Aberta</option><option value="Puntiforme">Puntiforme</option></select></div>',
      '<div><label>Medida Posterior</label><input id="fp_val" type="number" min="0" step="0.1" placeholder="Ex: 0.5"></div>',
      '<div><label>Unidade Posterior</label><select id="fp_unid"><option value="cm">cm</option><option value="polpa(s) digital(ais)">polpa(s) digital(ais)</option></select></div>',
    '</div>',
  '</fieldset>',

  '<fieldset>',
    '<legend>Cálculo de Ganho Ponderal</legend>',
    '<div class="grid">',
      '<div>',
        '<label>Comparar peso com</label>',
        '<select id="tipo_ganho">',
          '<option value="anterior" selected>Última consulta</option>',
          '<option value="nasc">Nascimento</option>',
        '</select>',
      '</div>',
      '<div><label id="lbl_peso_ref">Peso da última consulta (kg)</label><input id="peso_ref" type="number" min="0" step=".001"></div>',
    '</div>',
  '</fieldset>',

  '<button id="calcular_antropo">Calcular Antropometria & Gerar Gráficos</button>',
  '<div id="resultado_antropo" class="resultado">Preencha os campos e clique em calcular.</div>',

  '<hr style="margin: 30px 0; border: 0; border-top: 2px solid var(--background-modifier-border);">',

  '<h3>3. Exame Físico Pediátrico Especializado</h3>',

  '<fieldset>',
    '<legend>Ausculta Cardiovascular</legend>',
    '<div class="grid-2">',
      '<div><label>Frequência Cardíaca (bpm)</label><input id="fc" type="number" placeholder="Ex: 120"></div>',
      '<div><label>Ausculta Cardíaca (Descrição)</label><input id="ac_desc" type="text" placeholder="Ex: RCR em 2BC, normofonéticas, sem sopros"></div>',
    '</div>',
  '</fieldset>',

  '<fieldset>',
    '<legend>Ausculta Pulmonar</legend>',
    '<div class="grid-2">',
      '<div><label>Frequência Respiratória (ipm)</label><input id="fr" type="number" placeholder="Ex: 40"></div>',
      '<div><label>Ausculta Pulmonar</label><select id="ap_select"><option value="MVFD SRA bilateralmente">MVFD SRA bilateralmente</option><option value="OUTRO">Outro (Descrever)</option></select></div>',
    '</div>',
    '<div id="ap_outro_div" style="margin-top:10px; display:none;"><label>Descrição da Ausculta Pulmonar</label><input id="ap_desc" type="text" placeholder="Descreva as alterações pulmonares..."></div>',
  '</fieldset>',

  '<fieldset>',
    '<legend>Otorrinolaringologia (ORL)</legend>',
    '<div style="margin-bottom:12px;">',
      '<label>Otoscopia</label>',
      '<select id="oto_select"><option value="Membrana íntegra e translúcida bilateralmente">Membrana íntegra e translúcida bilateralmente</option><option value="OUTRO">Outro (Descrever)</option></select>',
      '<input id="oto_outro" type="text" placeholder="Descreva a otoscopia OD/OE..." style="margin-top:6px; display:none;">',
    '</div>',

    '<div style="margin-bottom:12px;">',
      '<label>Rinoscopia</label>',
      '<select id="rino_select"><option value="Mucosa íntegra, hidratada e sem lesões">Mucosa íntegra, hidratada e sem lesões</option><option value="OUTRO">Outro (Descrever)</option></select>',
      '<input id="rino_outro" type="text" placeholder="Descreva a rinoscopia..." style="margin-top:6px; display:none;">',
    '</div>',

    '<div>',
      '<label>Oroscopia</label>',
      '<select id="oro_select"><option value="Mucosa hidratada, normocorada e íntegra, ausência de hipertrofia de tonsilas">Mucosa hidratada, normocorada e íntegra, ausência de hipertrofia de tonsilas</option><option value="OUTRO">Outro (Descrever)</option></select>',
      '<input id="oro_outro" type="text" placeholder="Descreva a oroscopia..." style="margin-top:6px; display:none;">',
    '</div>',
  '</fieldset>',

  '<fieldset>',
    '<legend>Genitália & Estadiamento de Tanner</legend>',
    '<div id="dnpm_genitalia_masc" class="grid">',
      '<div><label>Estadiamento Genital (Tanner G)</label><select id="tanner_g"><option value="G1 (Infantil)">G1 - Infantil</option><option value="G2 (Aumento escrotal/testículos)">G2 - Aumento escrotal</option><option value="G3 (Aumento do pênis em comprimento)">G3 - Pênis em comprimento</option><option value="G4 (Aumento em diâmetro e glande)">G4 - Pênis em diâmetro</option><option value="G5 (Adulto)">G5 - Adulto</option></select></div>',
      '<div><label>Estadiamento Pubiano Masculino (Tanner P)</label><select id="tanner_pm"><option value="P1 (Ausente)">P1 - Ausente</option><option value="P2 (Pelos escassos na base do pênis)">P2 - Pelos escassos</option><option value="P3 (Pelos mais espessos)">P3 - Espessos</option><option value="P4 (Tipo adulto, área reduzida)">P4 - Tipo adulto reduzido</option><option value="P5 (Distribuição adulta)">P5 - Adulto</option></select></div>',
    '</div>',

    '<div id="dnpm_genitalia_fem" class="grid" style="display:none;">',
      '<div><label>Estadiamento Mamário (Tanner M)</label><select id="tanner_m"><option value="M1 (Infantil)">M1 - Infantil</option><option value="M2 (Broto mamário)">M2 - Broto mamário</option><option value="M3 (Aumento de mama/aréola)">M3 - Elevação de mama</option><option value="M4 (Projeção da aréola)">M4 - Projeção da aréola</option><option value="M5 (Adulta)">M5 - Adulta</option></select></div>',
      '<div><label>Estadiamento Pubiano Feminino (Tanner P)</label><select id="tanner_pf"><option value="P1 (Ausente)">P1 - Ausente</option><option value="P2 (Pelos escassos em grandes lábios)">P2 - Pelos escassos</option><option value="P3 (Pelos mais espessos na sínfise)">P3 - Sínfise púbica</option><option value="P4 (Tipo adulto, área reduzida)">P4 - Tipo adulto reduzido</option><option value="P5 (Distribuição adulta)">P5 - Adulto</option></select></div>',
    '</div>',

    '<div style="margin-top:10px;"><label>Exame Físico da Genitália (Descrição Livre)</label><input id="gen_desc_livre" type="text" placeholder="Ex: Testículos tópicos na bolsa escrotal, pênis sem alterações / Genitália típica sem lesões"></div>',
  '</fieldset>',

  '<hr style="margin: 30px 0; border: 0; border-top: 2px solid var(--background-modifier-border);">',

  '<h3>4. Vigilância do Desenvolvimento Neuropsicomotor (DNPM)</h3>',
  '<div id="aviso_idade_dnpm" style="font-size:0.9em; margin-bottom:12px; color:var(--text-muted);">* O checklist da faixa etária atual será expandido automaticamente após o cálculo da antropometria.</div>',
  '<div id="dnpm_container"></div>',

  '<button id="calcular_dnpm">Avaliar Desenvolvimento (DNPM)</button>',
  '<div id="resultado_dnpm" class="resultado">Preencha os marcos do desenvolvimento e clique em avaliar.</div>',

  '<hr style="margin: 30px 0; border: 0; border-top: 2px solid var(--background-modifier-border);">',

  '<h3>5. Histórico & Carteira de Vacinação (PNI / Ministério da Saúde)</h3>',
  '<div class="alerta-vacina">',
    '<strong>⚠️ Contraindicações & Alertas Rápidos:</strong><br>',
    '• <strong>Vacinas de Vírus Vivo (BCG, Rotavírus, Febre Amarela, Tríplice Viral, Varicela):</strong> Contraindicadas em imunodeficiência primária ou adquirida grave e corticoterapia imunossupressora.<br>',
    '• <strong>BCG:</strong> Adiar se RN com peso &lt; 2.000g até atingir 2 kg.<br>',
    '• <strong>Rotavírus (VRH):</strong> Limites RÍGIDOS de idade: 1ª dose até 11m 29d | 2ª dose até 23m 29d. Contraindicada se história de intussuscepção intestinal ou malformação TGI.<br>',
    '• <strong>Pentavalente / DTP:</strong> Se convulsões ou colapso circulatório/hipotônico pós-dose prévia, indicar DTPa (acelular no CRIE). Se encefalopatia em até 7 dias, indicar DT.',
  '</div>',
  '<div id="vacinas_container"></div>',

  '<button id="validar_vacinas">Validar Histórico Vacinal</button>',
  '<div id="resultado_vacinas" class="resultado">Marque as vacinas administradas e clique em validar.</div>',

  '<hr style="margin: 30px 0; border: 0; border-top: 2px solid var(--background-modifier-border);">',

  '<h3>6. Relatório Médico para Prontuário</h3>',
  '<button id="gerar_relatorio" style="background:#27ae60;">📋 Gerar Relatório Clínico Completo</button>',
  '<button id="copiar_relatorio" style="background:#2980b9;">📄 Copiar para Área de Transferência</button>',
  '<div id="box_relatorio" class="relatorio-box" style="margin-top:10px;">Clique no botão acima para compilar o prontuário.</div>'
].join("");

wrapper.appendChild(bodyDiv);
dv.container.appendChild(wrapper);

const app = dv.container.querySelector("#pueri-full-app");
const $ = id => app.querySelector("#" + id);

const hoje = new Date();
$("data").value = hoje.getFullYear() + "-" + String(hoje.getMonth()+1).padStart(2,"0") + "-" + String(hoje.getDate()).padStart(2,"0");

$("sexo").addEventListener("change", (e) => {
  if (e.target.value === "F") {
    $("dnpm_genitalia_fem").style.display = "grid";
    $("dnpm_genitalia_masc").style.display = "none";
  } else {
    $("dnpm_genitalia_fem").style.display = "none";
    $("dnpm_genitalia_masc").style.display = "grid";
  }
});

$("ap_select").addEventListener("change", (e) => {
  $("ap_outro_div").style.display = e.target.value === "OUTRO" ? "block" : "none";
});
$("oto_select").addEventListener("change", (e) => {
  $("oto_outro").style.display = e.target.value === "OUTRO" ? "block" : "none";
});
$("rino_select").addEventListener("change", (e) => {
  $("rino_outro").style.display = e.target.value === "OUTRO" ? "block" : "none";
});
$("oro_select").addEventListener("change", (e) => {
  $("oro_outro").style.display = e.target.value === "OUTRO" ? "block" : "none";
});

const referencias = {
  M: {
    peso_preterm: [[24,0.6],[28,1.1],[32,1.8],[36,2.6],[40,3.4],[44,4.5],[48,5.6],[50,6.2]],
    est_preterm:  [[24,31.0],[28,36.5],[32,42.0],[36,46.5],[40,50.0],[44,54.5],[48,58.0],[50,60.0]],
    pc_preterm:   [[24,22.0],[28,25.5],[32,29.0],[36,32.5],[40,34.5],[44,37.0],[48,39.0],[50,40.0]],
    peso_0_2: [[0,3.3],[3,6.4],[6,7.9],[9,8.9],[12,9.6],[18,10.9],[24,12.2]],
    est_0_2:  [[0,49.9],[3,61.4],[6,67.6],[9,72.0],[12,75.7],[18,82.3],[24,87.8]],
    pc_0_2:   [[0,34.5],[3,40.5],[6,43.3],[9,45.0],[12,46.1],[18,47.7],[24,48.6]],
    imc_0_2:  [[0,13.4],[3,16.9],[6,17.2],[9,16.8],[12,16.8],[18,16.2],[24,15.7]],
    peso_2_5: [[24,12.2],[30,13.3],[36,14.3],[42,15.3],[48,16.3],[54,17.3],[60,18.3]],
    est_2_5:  [[24,87.1],[30,91.9],[36,96.1],[42,99.9],[48,103.3],[54,106.7],[60,110.0]],
    imc_2_5:  [[24,16.0],[30,15.7],[36,15.5],[42,15.4],[48,15.3],[54,15.3],[60,15.3]],
    peso_5_10:[[60,18.3],[72,20.5],[84,22.9],[96,25.6],[108,28.6],[120,32.0]],
    est_5_10: [[60,110.0],[72,116.0],[84,121.7],[96,127.3],[108,132.6],[120,137.8]],
    imc_5_10: [[60,15.3],[72,15.3],[84,15.5],[96,15.9],[108,16.4],[120,17.0]]
  },
  F: {
    peso_preterm: [[24,0.55],[28,1.0],[32,1.65],[36,2.45],[40,3.2],[44,4.2],[48,5.1],[50,5.7]],
    est_preterm:  [[24,30.5],[28,35.5],[32,41.0],[36,45.5],[40,49.0],[44,53.5],[48,57.0],[50,59.0]],
    pc_preterm:   [[24,21.5],[28,24.8],[32,28.2],[36,31.8],[40,33.9],[44,36.2],[48,38.2],[50,39.2]],
    peso_0_2: [[0,3.2],[3,5.8],[6,7.3],[9,8.2],[12,8.9],[18,10.2],[24,11.5]],
    est_0_2:  [[0,49.1],[3,59.8],[6,65.7],[9,70.1],[12,74.0],[18,80.7],[24,86.4]],
    pc_0_2:   [[0,33.9],[3,39.5],[6,42.2],[9,43.8],[12,44.9],[18,46.3],[24,47.2]],
    imc_0_2:  [[0,13.3],[3,16.3],[6,16.7],[9,16.5],[12,16.1],[18,15.6],[24,15.3]],
    peso_2_5: [[24,11.5],[30,12.7],[36,13.9],[42,15.0],[48,16.1],[54,17.2],[60,18.2]],
    est_2_5:  [[24,85.7],[30,90.7],[36,95.1],[42,99.0],[48,102.7],[54,106.2],[60,109.4]],
    imc_2_5:  [[24,15.7],[30,15.4],[36,15.3],[42,15.2],[48,15.2],[54,15.2],[60,15.3]],
    peso_5_10:[[60,18.2],[72,20.2],[84,22.4],[96,25.0],[108,28.2],[120,31.9]],
    est_5_10: [[60,109.4],[72,115.5],[84,121.1],[96,126.6],[108,131.9],[120,137.3]],
    imc_5_10: [[60,15.3],[72,15.3],[84,15.4],[96,15.7],[108,16.3],[120,17.0]]
  }
};

const marcosDNPM = [
  { id: "f0_1", min: 0, max: 1, label: "0 a 1 mês", marcos: [
    { id: "m1_1", texto: "Postura flexionada de recém-nascido", alerta: false },
    { id: "m1_2", texto: "Observa o rosto de quem olha para ele", alerta: false },
    { id: "m1_3", texto: "Reage ao som de campainha/chocalho", alerta: false },
    { id: "m1_4", texto: "Ausência de reflexo de Moro", alerta: true },
    { id: "m1_5", texto: "Microcefalia ou Macrocefalia evidente", alerta: true }
  ]},
  { id: "f1_2", min: 1, max: 2, label: "1 a 2 meses", marcos: [
    { id: "m2_1", texto: "Eleva a cabeça momentaneamente em prono", alerta: false },
    { id: "m2_2", texto: "Sorriso social quando estimulado", alerta: false },
    { id: "m2_3", texto: "Emite sons/vocalizações curtas", alerta: false },
    { id: "m2_4", texto: "Acompanha objetos com o olhar até a linha média", alerta: false },
    { id: "m2_5", texto: "Hipotonia muscular acentuada", alerta: true }
  ]},
  { id: "f2_4", min: 2, max: 4, label: "2 a 4 meses", marcos: [
    { id: "m4_1", texto: "Sustenta a cabeça de forma firme ao estar sentado", alerta: false },
    { id: "m4_2", texto: "Responde ao contato verbal sorrindo/gorgolejando", alerta: false },
    { id: "m4_3", texto: "Abre as mãos espontaneamente e junta-as no centro", alerta: false },
    { id: "m4_4", texto: "Leva objetos voluntariamente à boca", alerta: false },
    { id: "m4_5", texto: "Assimetria postural persistente de membros", alerta: true }
  ]},
  { id: "f4_6", min: 4, max: 6, label: "4 a 6 meses", marcos: [
    { id: "m6_1", texto: "Rola de costas para o lado ou de bruços", alerta: false },
    { id: "m6_2", texto: "Alcança e pega brinquedos/objetos voluntariamente", alerta: false },
    { id: "m6_3", texto: "Muda a atenção ao ouvir o som do próprio nome", alerta: false },
    { id: "m6_4", texto: "Lalia e emite sílabas como 'da-da', 'ba-ba'", alerta: false },
    { id: "m6_5", texto: "Mãos continuamente fechadas com polegar aduto", alerta: true }
  ]},
  { id: "f6_9", min: 6, max: 9, label: "6 a 9 meses", marcos: [
    { id: "m9_1", texto: "Senta-se sozinho sem apoio de mãos", alerta: false },
    { id: "m9_2", texto: "Passa objetos de uma mão para a outra", alerta: false },
    { id: "m9_3", texto: "Realiza preensão radial ou em pinça inferior", alerta: false },
    { id: "m9_4", texto: "Estranha pessoas desconhecidas", alerta: false },
    { id: "m9_5", texto: "Não mantém o apoio do próprio peso nas pernas", alerta: true }
  ]},
  { id: "f9_12", min: 9, max: 12, label: "9 a 12 meses", marcos: [
    { id: "m12_1", texto: "Fica em pé segurando-se nos móveis", alerta: false },
    { id: "m12_2", texto: "Executa a preensão em pinça fina (polegar e indicador)", alerta: false },
    { id: "m12_3", texto: "Acena 'tchau' ou faz 'palminhas'", alerta: false },
    { id: "m12_4", texto: "Fala de 1 a 3 palavras com significado (ex: 'mamãe')", alerta: false },
    { id: "m12_5", texto: "Ausência de engatinhar ou arrastar eficiente", alerta: true }
  ]},
  { id: "f12_15", min: 12, max: 15, label: "12 a 15 meses", marcos: [
    { id: "m15_1", texto: "Carrega objetos enquanto caminha sem ajuda", alerta: false },
    { id: "m15_2", texto: "Coloca blocos em um recipiente/copo", alerta: false },
    { id: "m15_3", texto: "Aponta com o indicador para mostrar o que deseja", alerta: false },
    { id: "m15_4", texto: "Imita gestos simples de adultos em brincadeiras", alerta: false },
    { id: "m15_5", texto: "Incapacidade de andar sem apoio até 15 meses", alerta: true }
  ]},
  { id: "f15_18", min: 15, max: 18, label: "15 a 18 meses", marcos: [
    { id: "m18_1", texto: "Anda sozinho com bom equilíbrio", alerta: false },
    { id: "m18_2", texto: "Constrói torre com 3 a 4 cubos", alerta: false },
    { id: "m18_3", texto: "Vocabulário ativo de pelo menos 6 palavras", alerta: false },
    { id: "m18_4", texto: "Usa colher ou garfo levando comida à boca", alerta: false },
    { id: "m18_5", texto: "Não atende pelo nome ou evita contato visual", alerta: true }
  ]},
  { id: "f18_24", min: 18, max: 24, label: "18 a 24 meses", marcos: [
    { id: "m24_1", texto: "Corre e chuta uma bola mantendo o equilíbrio", alerta: false },
    { id: "m24_2", texto: "Junta 2 palavras para formar frases curtas (ex: 'quer água')", alerta: false },
    { id: "m24_3", texto: "Tira peças simples de vestuário sem ajuda", alerta: false },
    { id: "m24_4", texto: "Demonstra interesse por brincar com outras crianças", alerta: false },
    { id: "m24_5", texto: "Perda abrupta de habilidades de fala adquiridas", alerta: true }
  ]},
  { id: "f24_36", min: 24, max: 36, label: "2 a 3 anos (24 a 36m)", marcos: [
    { id: "m36_1", texto: "Pula com os dois pés juntos no mesmo lugar", alerta: false },
    { id: "m36_2", texto: "Desenha círculos ou linhas verticais em papel", alerta: false },
    { id: "m36_3", texto: "Forma frases completas de 3 a 4 palavras", alerta: false },
    { id: "m36_4", texto: "Veste roupas simples com supervisão", alerta: false },
    { id: "m36_5", texto: "Fala predominantemente ininteligível para estanhos", alerta: true }
  ]}
];

const calendarioVacinas = [
  {
    periodo: "Ao Nascer", minMeses: 0,
    vacinas: [
      { id: "bcg", nome: "BCG (Dose única)" },
      { id: "hepb_0", nome: "Hepatite B (Dose ao nascer)" }
    ]
  },
  {
    periodo: "2 Meses", minMeses: 2,
    vacinas: [
      { id: "penta_1", nome: "Pentavalente (1ª dose)" },
      { id: "vip_1", nome: "VIP / Polio Inativada (1ª dose)" },
      { id: "pneumo_1", nome: "Pneumocócica 10V (1ª dose)" },
      { id: "rota_1", nome: "Rotavírus Humano VRH (1ª dose)" }
    ]
  },
  {
    periodo: "3 Meses", minMeses: 3,
    vacinas: [
      { id: "meningo_1", nome: "Meningocócica C (1ª dose)" }
    ]
  },
  {
    periodo: "4 Meses", minMeses: 4,
    vacinas: [
      { id: "penta_2", nome: "Pentavalente (2ª dose)" },
      { id: "vip_2", nome: "VIP / Polio Inativada (2ª dose)" },
      { id: "pneumo_2", nome: "Pneumocócica 10V (2ª dose)" },
      { id: "rota_2", nome: "Rotavírus Humano VRH (2ª dose)" }
    ]
  },
  {
    periodo: "5 Meses", minMeses: 5,
    vacinas: [
      { id: "meningo_2", nome: "Meningocócica C (2ª dose)" }
    ]
  },
  {
    periodo: "6 Meses", minMeses: 6,
    vacinas: [
      { id: "penta_3", nome: "Pentavalente (3ª dose)" },
      { id: "vip_3", nome: "VIP / Polio Inativada (3ª dose)" },
      { id: "covid_1", nome: "COVID-19 (1ª dose)" }
    ]
  },
  {
    periodo: "7 a 9 Meses", minMeses: 7,
    vacinas: [
      { id: "covid_2", nome: "COVID-19 (2ª dose)" },
      { id: "fa_1", nome: "Febre Amarela (1ª dose aos 9m)" }
    ]
  },
  {
    periodo: "12 Meses (1 Ano)", minMeses: 12,
    vacinas: [
      { id: "triplice_1", nome: "Tríplice Viral - SCR (1ª dose)" },
      { id: "pneumo_ref", nome: "Pneumocócica 10V (Reforço)" },
      { id: "meningo_ref", nome: "Meningocócica C (Reforço)" }
    ]
  },
  {
    periodo: "15 Meses", minMeses: 15,
    vacinas: [
      { id: "dtp_ref1", nome: "DTP / Tríplice Bacteriana (1º reforço)" },
      { id: "vip_ref1", nome: "VIP / Polio Inativada (1º reforço)" },
      { id: "hepa", nome: "Hepatite A (Dose única)" },
      { id: "tetraviral", nome: "Tetraviral ou SCR + Varicela (1ª dose)" }
    ]
  },
  {
    periodo: "4 Anos", minMeses: 48,
    vacinas: [
      { id: "dtp_ref2", nome: "DTP / Tríplice Bacteriana (2º reforço)" },
      { id: "vip_ref2", nome: "VIP / Polio Inativada (2º reforço)" },
      { id: "fa_ref", nome: "Febre Amarela (Reforço)" },
      { id: "varicela_2", nome: "Varicela (2ª dose)" }
    ]
  }
];

function renderizarDNPM() {
  const container = $("dnpm_container");
  container.innerHTML = "";

  marcosDNPM.forEach(faixa => {
    const details = document.createElement("details");
    details.id = "details_" + faixa.id;
    
    let htmlMarcos = faixa.marcos.map(m => 
      '<div class="checkbox-item" style="margin:6px 0;">' +
        '<input type="checkbox" id="chk_' + m.id + '" data-faixa="' + faixa.id + '" data-alerta="' + m.alerta + '">' +
        '<label for="chk_' + m.id + '">' + m.texto + (m.alerta ? ' <span class="badge-dnpm badge-alerta">ALERTA/SINAL DE RISCO</span>' : '') + '</label>' +
      '</div>'
    ).join("");

    details.innerHTML = '<summary>' + faixa.label + '</summary><div style="padding-top:10px;">' + htmlMarcos + '</div>';
    container.appendChild(details);
  });
}
renderizarDNPM();

function renderizarVacinas() {
  const container = $("vacinas_container");
  container.innerHTML = "";

  calendarioVacinas.forEach(p => {
    const details = document.createElement("details");
    details.id = "vac_details_" + p.minMeses;
    details.open = true;

    let htmlVac = p.vacinas.map(v => 
      '<div class="checkbox-item" style="margin:6px 0;">' +
        '<input type="checkbox" id="vac_' + v.id + '" data-minmeses="' + p.minMeses + '" data-nome="' + v.nome + '">' +
        '<label for="vac_' + v.id + '">' + v.nome + '</label>' +
      '</div>'
    ).join("");

    details.innerHTML = '<summary>' + p.periodo + '</summary><div style="padding-top:10px;">' + htmlVac + '</div>';
    container.appendChild(details);
  });
}
renderizarVacinas();

function interpolar(pontos, x) {
  const i = pontos.findIndex(p => p[0] >= x);
  if (i === 0) return pontos[0][1];
  if (i < 0) return pontos[pontos.length-1][1];
  const [x0,y0] = pontos[i-1];
  const [x1,y1] = pontos[i];
  return y0 + (y1-y0)*(x-x0)/(x1-x0);
}

function carregarTabelasLMS(sexo) {
  const base = referencias[sexo];
  const tab = {};
  const configs = [
    { key: "peso_preterm", start: 24, end: 50, S: 0.13, L: -0.1 },
    { key: "est_preterm",  start: 24, end: 50, S: 0.04, L: 1.0 },
    { key: "pc_preterm",   start: 24, end: 50, S: 0.035, L: 1.0 },
    { key: "peso_0_2", start: 0, end: 24, S: 0.115, L: -0.15 },
    { key: "est_0_2",  start: 0, end: 24, S: 0.038, L: 1.0 },
    { key: "pc_0_2",   start: 0, end: 24, S: 0.033, L: 1.0 },
    { key: "imc_0_2",  start: 0, end: 24, S: 0.085, L: -0.35 },
    { key: "peso_2_5", start: 24, end: 60, S: 0.12, L: -0.1 },
    { key: "est_2_5",  start: 24, end: 60, S: 0.04, L: 1.0 },
    { key: "imc_2_5",  start: 24, end: 60, S: 0.09, L: -0.3 },
    { key: "peso_5_10", start: 60, end: 120, S: 0.14, L: -0.2 },
    { key: "est_5_10",  start: 60, end: 120, S: 0.045, L: 1.0 },
    { key: "imc_5_10",  start: 60, end: 120, S: 0.11, L: -0.4 }
  ];

  for (const cfg of configs) {
    const totalSteps = Math.round((cfg.end - cfg.start) * 2);
    tab[cfg.key] = Array.from({length: totalSteps + 1}, (_, i) => {
      const x = cfg.start + (i / 2);
      return { x, L: cfg.L, M: interpolar(base[cfg.key], x), S: cfg.S };
    });
  }
  return tab;
}

function calcYfromZ(lms, z) {
  const L = lms.L, M = lms.M, S = lms.S;
  if (Math.abs(L) < 1e-8) return M * Math.exp(S * z);
  return M * Math.pow(1 + L * S * z, 1 / L);
}

function idadeCalendario(nasc, data) {
  const [a,m,d] = nasc.split("-").map(Number);
  const [aa,mm,dd] = data.split("-").map(Number);
  if (Date.UTC(aa,mm-1,dd) < Date.UTC(a,m-1,d)) return null;

  let anos = aa-a, meses = mm-m, dias = dd-d;
  if (dias < 0) {
    meses--;
    dias += new Date(aa,mm-1,0).getDate();
  }
  if (meses < 0) {
    anos--;
    meses += 12;
  }
  return {anos,meses,dias};
}

function diasEntre(a,b) {
  const [y,m,d] = a.split("-").map(Number);
  const [yy,mm,dd] = b.split("-").map(Number);
  return Math.round((Date.UTC(yy,mm-1,dd)-Date.UTC(y,m-1,d))/86400000);
}

function idadeMeses(nasc,data) {
  const i = idadeCalendario(nasc,data);
  return i ? i.anos*12+i.meses+i.dias/30.4375 : -1;
}

function lmsAt(tab, x) {
  if (!tab) return null;
  const clampedX = Math.max(tab[0].x, Math.min(tab[tab.length-1].x, x));
  const i = tab.findIndex(p => p.x >= clampedX);
  if (i === 0) return Object.assign({}, tab[0]);
  if (i < 0) return Object.assign({}, tab[tab.length-1]);
  const a = tab[i-1], b = tab[i], f = (clampedX-a.x)/(b.x-a.x);
  return { x: clampedX, L:a.L+(b.L-a.L)*f, M:a.M+(b.M-a.M)*f, S:a.S+(b.S-a.S)*f };
}

function zScore(value, lms) {
  if (!(value > 0) || !lms) return null;
  const L = lms.L, M = lms.M, S = lms.S;
  return Math.abs(L) < 1e-8 ? Math.log(value/M)/S : (Math.pow(value/M,L)-1)/(L*S);
}

function fmt(n,d=2) {
  return n == null || !Number.isFinite(n) ? "—" : n.toFixed(d).replace(".",",");
}

function getInfoPeso(z) {
  if (z == null) return { faixa: "—", desc: "—" };
  if (z > 2) return { faixa: "Z > +2", desc: "Peso elevado para a idade" };
  if (z >= -2) return { faixa: "[-2, +2]", desc: "Peso adequado para a idade" };
  if (z >= -3) return { faixa: "[-3, -2)", desc: "Baixo peso para a idade" };
  return { faixa: "Z < -3", desc: "Muito baixo peso para a idade" };
}

function getInfoEst(z) {
  if (z == null) return { faixa: "—", desc: "—" };
  if (z >= -2) return { faixa: "Z ≥ -2", desc: "Estatura/Comprimento adequado" };
  if (z >= -3) return { faixa: "[-3, -2)", desc: "Baixa estatura para a idade" };
  return { faixa: "Z < -3", desc: "Muito baixa estatura para a idade" };
}

function getInfoIMC(z) {
  if (z == null) return { faixa: "—", desc: "—" };
  if (z > 3) return { faixa: "Z > +3", desc: "Obesidade Severa" };
  if (z > 2) return { faixa: "(+2, +3]", desc: "Obesidade / Sobrepeso" };
  if (z > 1) return { faixa: "(+1, +2]", desc: "Risco de Sobrepeso" };
  if (z >= -2) return { faixa: "[-2, +1]", desc: "Eutrofia (Adequado)" };
  if (z >= -3) return { faixa: "[-3, -2)", desc: "Magreza" };
  return { faixa: "Z < -3", desc: "Magreza Acentuada" };
}

function getInfoPC(z) {
  if (z == null) return { faixa: "—", desc: "—" };
  if (z > 2) return { faixa: "Z > +2", desc: "Macrocefalia / Acima do esperado" };
  if (z >= -2) return { faixa: "[-2, +2]", desc: "Perímetro Cefálico Adequado" };
  return { faixa: "Z < -2", desc: "Microcefalia / Abaixo do esperado" };
}

function gerarSVG(tab, tabKey, idadeAtiva, valAtual, zVal, infoObj, titulo, minM, maxM, ticksX, isAplicavel, labelIdadeUsada, sexo) {
  const t = tab[tabKey];
  if (!t) return "";

  const w = 520, h = 270, padL = 45, padR = 50, padT = 25, padB = 35;
  const series = t.map(lms => ({
    x: lms.x, z3: calcYfromZ(lms, 3), z2: calcYfromZ(lms, 2), z0: calcYfromZ(lms, 0), zm2: calcYfromZ(lms, -2), zm3: calcYfromZ(lms, -3)
  }));

  const allY = series.flatMap(s => [s.z3, s.zm3]);
  if (valAtual != null && isAplicavel) allY.push(valAtual);
  
  const minY = Math.min(...allY) * 0.95;
  const maxY = Math.max(...allY) * 1.05;

  const getX = m => padL + (Math.max(minM, Math.min(maxM, m)) - minM) / (maxM - minM) * (w - padL - padR);
  const getY = v => h - padB - ((v - minY) / (maxY - minY)) * (h - padT - padB);

  const ptsPlus3 = series.map(s => getX(s.x) + "," + getY(s.z3)).join(" ");
  const ptsPlus2 = series.map(s => getX(s.x) + "," + getY(s.z2)).join(" ");
  const ptsMed   = series.map(s => getX(s.x) + "," + getY(s.z0)).join(" ");
  const ptsMinus2 = series.map(s => getX(s.x) + "," + getY(s.zm2)).join(" ");
  const ptsMinus3 = series.map(s => getX(s.x) + "," + getY(s.zm3)).join(" ");

  const lastS = series[series.length - 1];
  const unitLabel = tabKey.includes("preterm") ? "sem" : "m";

  const gridX = ticksX.map(m => 
    '<line x1="' + getX(m) + '" y1="' + padT + '" x2="' + getX(m) + '" y2="' + (h-padB) + '" stroke="var(--background-modifier-border)" stroke-width="0.8" stroke-dasharray="2,2"/>' +
    '<text x="' + getX(m) + '" y="' + (h-12) + '" font-size="9" fill="var(--text-muted)" text-anchor="middle">' + m + unitLabel + '</text>'
  ).join("");

  let pontoPaciente = "";
  if (valAtual != null && isAplicavel) {
    const px = getX(idadeAtiva);
    const py = getY(valAtual);
    pontoPaciente = '<circle cx="' + px + '" cy="' + py + '" r="6" fill="#e74c3c" stroke="#ffffff" stroke-width="2" />';
  }

  const cardClass = isAplicavel ? "chart-card" : "chart-card disabled";
  const overlay = !isAplicavel ? '<div class="na-overlay">Fora da Faixa Etária (' + minM + ' a ' + maxM + unitLabel + ')</div>' : "";
  const statusFooter = isAplicavel ? 'Escore-Z: <strong>' + fmt(zVal) + '</strong> | Faixa: <strong>' + infoObj.faixa + '</strong> (' + infoObj.desc + ')' : 'Gráfico inativo para esta idade.';

  return '<div class="' + cardClass + '">' +
      overlay +
      '<div style="overflow:hidden;">' +
        '<span class="chart-badge">' + labelIdadeUsada + '</span>' +
        '<div class="chart-title">' + titulo + ' (' + (sexo === "M" ? "Menino" : "Menina") + ')</div>' +
      '</div>' +
      '<svg viewBox="0 0 ' + w + ' ' + h + '">' +
        gridX +
        '<line x1="' + padL + '" y1="' + (h-padB) + '" x2="' + (w-padR) + '" y2="' + (h-padB) + '" stroke="var(--text-normal)" stroke-width="1.2"/>' +
        '<line x1="' + padL + '" y1="' + padT + '" x2="' + padL + '" y2="' + (h-padB) + '" stroke="var(--text-normal)" stroke-width="1.2"/>' +
        '<polyline fill="none" stroke="#e74c3c" stroke-width="1.2" stroke-dasharray="3,3" points="' + ptsPlus3 + '" />' +
        '<polyline fill="none" stroke="#f39c12" stroke-width="1.5" stroke-dasharray="4,3" points="' + ptsPlus2 + '" />' +
        '<polyline fill="none" stroke="#27ae60" stroke-width="2.2" points="' + ptsMed + '" />' +
        '<polyline fill="none" stroke="#f39c12" stroke-width="1.5" stroke-dasharray="4,3" points="' + ptsMinus2 + '" />' +
        '<polyline fill="none" stroke="#e74c3c" stroke-width="1.2" stroke-dasharray="3,3" points="' + ptsMinus3 + '" />' +
        '<text x="' + (w-padR+6) + '" y="' + (getY(lastS.z3)+3) + '" font-size="9" font-weight="bold" fill="#e74c3c">Z +3</text>' +
        '<text x="' + (w-padR+6) + '" y="' + (getY(lastS.z2)+3) + '" font-size="9" font-weight="bold" fill="#f39c12">Z +2</text>' +
        '<text x="' + (w-padR+6) + '" y="' + (getY(lastS.z0)+3) + '" font-size="9" font-weight="bold" fill="#27ae60">Z 0</text>' +
        '<text x="' + (w-padR+6) + '" y="' + (getY(lastS.zm2)+3) + '" font-size="9" font-weight="bold" fill="#f39c12">Z -2</text>' +
        '<text x="' + (w-padR+6) + '" y="' + (getY(lastS.zm3)+3) + '" font-size="9" font-weight="bold" fill="#e74c3c">Z -3</text>' +
        pontoPaciente +
      '</svg>' +
      '<div style="font-size:0.85em; color:var(--text-muted); margin-top:6px; text-align:right;">' +
        statusFooter +
      '</div>' +
    '</div>';
}

$("tipo_ganho").addEventListener("change", (e) => {
  if (e.target.value === "nasc") {
    $("lbl_peso_ref").textContent = "Peso de nascimento (kg)";
  } else {
    $("lbl_peso_ref").textContent = "Peso da última consulta (kg)";
  }
});

let cacheUltimaAntropometria = null;

$("calcular_antropo").addEventListener("click", () => {
  const nome = $("nome_paciente").value || "Criança";
  const sexo = $("sexo").value;
  const nasc = $("nasc").value;
  const data = $("data").value;
  const dataAnt = $("data_ant").value;
  const ig = $("ig").value === "" ? 40 : Number($("ig").value);

  if (!nasc || !data) {
    $("resultado_antropo").textContent = "Preencha a data de nascimento e a data da consulta atual.";
    return;
  }

  const age = idadeCalendario(nasc, data);
  if (!age) {
    $("resultado_antropo").textContent = "A data da consulta não pode ser anterior ao nascimento.";
    return;
  }

  let mCrono = idadeMeses(nasc, data);
  let semanasVida = diasEntre(nasc, data) / 7;
  let semanasPosConcepcional = ig + semanasVida;
  
  let descontoSemanas = 40 - ig;
  let mCorrig = mCrono - (descontoSemanas / 4.345);
  let mInfantil = (ig < 37 && mCorrig <= 24) ? mCorrig : mCrono;

  if (semanasPosConcepcional < 40) {
    $("aviso_idade_dnpm").innerHTML = "Idade Pós-Concepcional: <strong>" + fmt(semanasPosConcepcional, 1) + " semanas</strong> (RN Pré-Termo em acompanhamento pós-natal).";
  } else {
    marcosDNPM.forEach(f => {
      const el = app.querySelector("#details_" + f.id);
      if (el) el.open = (mInfantil >= f.min && mInfantil < f.max);
    });
    $("aviso_idade_dnpm").innerHTML = "Idade de avaliação do DNPM: <strong>" + fmt(mInfantil, 1) + " meses</strong> " + (ig < 37 ? "(Idade Corrigida para Prematuro)" : "");
  }

  const isPretermActive = ig < 37 && semanasPosConcepcional < 40;
  const is0_2 = !isPretermActive && (mInfantil >= 0 && mInfantil <= 24);
  const is2_5 = !isPretermActive && (mCrono > 24 && mCrono <= 60);
  const is5_10 = !isPretermActive && (mCrono > 60 && mCrono <= 120);

  let lblPreterm = "Pós-Concepcional: " + fmt(semanasPosConcepcional, 1) + " sem";
  let lbl0_2 = (ig < 37 && mCorrig <= 24) ? "Idade Corrigida: " + fmt(mCorrig, 1) + "m" : "Idade Cronológica: " + fmt(mCrono, 1) + "m";
  let lbl2_5 = "Idade Cronológica: " + fmt(mCrono, 1) + "m";
  let lbl5_10 = "Idade Cronológica: " + fmt(mCrono, 1) + "m";

  const peso = $("peso").value === "" ? null : Number($("peso").value);
  const est = $("est").value === "" ? null : Number($("est").value);
  const pc = $("pc").value === "" ? null : Number($("pc").value);
  const pa = $("pa").value === "" ? null : Number($("pa").value);
  const pt = $("pt").value === "" ? null : Number($("pt").value);
  const imc = (peso != null && est != null) ? peso / Math.pow(est / 100, 2) : null;

  let ganhoStr = "Não calculado.";
  const tipo = $("tipo_ganho").value;
  const pesoRef = $("peso_ref").value === "" ? null : Number($("peso_ref").value);

  if (tipo === "nasc") {
    if (pesoRef != null && peso != null) {
      const dias = diasEntre(nasc, data);
      if (dias > 0) {
        const dif = (peso - pesoRef) * 1000;
        ganhoStr = "<strong>" + fmt(dif/dias, 1) + " g/dia</strong> (" + fmt(dif, 0) + " g em " + dias + " dias desde o nascimento)";
      }
    }
  } else {
    if (dataAnt && pesoRef != null && peso != null) {
      const dias = diasEntre(dataAnt, data);
      if (dias > 0) {
        const dif = (peso - pesoRef) * 1000;
        ganhoStr = "<strong>" + fmt(dif/dias, 1) + " g/dia</strong> (" + fmt(dif, 0) + " g em " + dias + " dias desde a última consulta)";
      }
    }
  }

  const tab = carregarTabelasLMS(sexo);

  const zP_Pre = (isPretermActive && peso) ? zScore(peso, lmsAt(tab.peso_preterm, semanasPosConcepcional)) : null;
  const zE_Pre = (isPretermActive && est)  ? zScore(est,  lmsAt(tab.est_preterm,  semanasPosConcepcional)) : null;
  const zC_Pre = (isPretermActive && pc)   ? zScore(pc,   lmsAt(tab.pc_preterm,   semanasPosConcepcional)) : null;

  const zP0_2 = (is0_2 && peso) ? zScore(peso, lmsAt(tab.peso_0_2, mInfantil)) : null;
  const zE0_2 = (is0_2 && est)  ? zScore(est,  lmsAt(tab.est_0_2,  mInfantil)) : null;
  const zI0_2 = (is0_2 && imc)  ? zScore(imc,  lmsAt(tab.imc_0_2,  mInfantil)) : null;
  const zC0_2 = (is0_2 && pc)   ? zScore(pc,   lmsAt(tab.pc_0_2,   mInfantil)) : null;

  const zP2_5 = (is2_5 && peso) ? zScore(peso, lmsAt(tab.peso_2_5, mCrono)) : null;
  const zE2_5 = (is2_5 && est)  ? zScore(est,  lmsAt(tab.est_2_5,  mCrono)) : null;
  const zI2_5 = (is2_5 && imc)  ? zScore(imc,  lmsAt(tab.imc_2_5,  mCrono)) : null;

  const zP5_10 = (is5_10 && peso) ? zScore(peso, lmsAt(tab.peso_5_10, mCrono)) : null;
  const zE5_10 = (is5_10 && est)  ? zScore(est,  lmsAt(tab.est_5_10,  mCrono)) : null;
  const zI5_10 = (is5_10 && imc)  ? zScore(imc,  lmsAt(tab.imc_5_10,  mCrono)) : null;

  const activeZ_P = isPretermActive ? zP_Pre : is0_2 ? zP0_2 : is2_5 ? zP2_5 : zP5_10;
  const activeZ_E = isPretermActive ? zE_Pre : is0_2 ? zE0_2 : is2_5 ? zE2_5 : zE5_10;
  const activeZ_I = isPretermActive ? null : is0_2 ? zI0_2 : is2_5 ? zI2_5 : zI5_10;

  cacheUltimaAntropometria = {
    activeZ_P, activeZ_E, activeZ_I,
    zC: isPretermActive ? zC_Pre : is0_2 ? zC0_2 : null,
    infoP: getInfoPeso(activeZ_P),
    infoE: getInfoEst(activeZ_E),
    infoI: getInfoIMC(activeZ_I),
    infoC: getInfoPC(isPretermActive ? zC_Pre : is0_2 ? zC0_2 : null),
    isPretermActive
  };

  let infoIdade = "<strong>Paciente:</strong> " + nome + " (" + (sexo === "M" ? "Masculino" : "Feminino") + ")<br>" +
                   "<strong>Idade Cronológica:</strong> " + age.anos + "a " + age.meses + "m " + age.dias + "d (" + Math.round(diasEntre(nasc,data)) + " dias)";
  if (ig < 37) {
    if (isPretermActive) {
      infoIdade += "<br><strong>Recém-nascido Pré-termo (" + ig + " sem):</strong> Idade Pós-Concepcional Atual = <strong>" + fmt(semanasPosConcepcional, 1) + " semanas</strong> (Curvas Fenton/INTERGROWTH)";
    } else {
      infoIdade += "<br><strong>Prematuro (" + ig + " sem):</strong> Idade Corrigida = " + fmt(mCorrig, 1) + " meses";
    }
  }

  $("resultado_antropo").innerHTML = 
    infoIdade + "<br>" +
    "<strong>Ganho Ponderal Diário:</strong> " + ganhoStr + "<br>" +
    "<strong>Medidas Complementares:</strong> Perímetro Abdominal = " + (pa ? pa + " cm" : "—") + " | Perímetro Torácico = " + (pt ? pt + " cm" : "—") + "<br><br>" +
    "<strong>📊 Resumo Antropométrico:</strong>" +
    "<table>" +
      "<thead>" +
        "<tr>" +
          "<th>Parâmetro</th>" +
          "<th>Medida</th>" +
          "<th>Z-Score Exato</th>" +
          "<th>Faixa Z</th>" +
          "<th>Classificação OMS/Caderneta</th>" +
        "</tr>" +
      "</thead>" +
      "<tbody>" +
        "<tr>" +
          "<td><strong>Peso para Idade</strong></td>" +
          "<td>" + (peso ? fmt(peso,3) + " kg" : "—") + "</td>" +
          "<td>" + fmt(activeZ_P) + "</td>" +
          "<td>" + getInfoPeso(activeZ_P).faixa + "</td>" +
          "<td>" + getInfoPeso(activeZ_P).desc + "</td>" +
        "</tr>" +
        "<tr>" +
          "<td><strong>Estatura/Comprimento</strong></td>" +
          "<td>" + (est ? fmt(est,1) + " cm" : "—") + "</td>" +
          "<td>" + fmt(activeZ_E) + "</td>" +
          "<td>" + getInfoEst(activeZ_E).faixa + "</td>" +
          "<td>" + getInfoEst(activeZ_E).desc + "</td>" +
        "</tr>" +
        "<tr>" +
          "<td><strong>IMC para Idade</strong></td>" +
          "<td>" + (imc && !isPretermActive ? fmt(imc,2) + " kg/m²" : "—") + "</td>" +
          "<td>" + (isPretermActive ? "N/A (Pré-termo)" : fmt(activeZ_I)) + "</td>" +
          "<td>" + (isPretermActive ? "—" : getInfoIMC(activeZ_I).faixa) + "</td>" +
          "<td>" + (isPretermActive ? "IMC não avaliado <40 semanas" : getInfoIMC(activeZ_I).desc) + "</td>" +
        "</tr>" +
        "<tr>" +
          "<td><strong>Perímetro Cefálico</strong></td>" +
          "<td>" + (pc ? fmt(pc,1) + " cm" : "—") + "</td>" +
          "<td>" + (isPretermActive ? fmt(zC_Pre) : is0_2 ? fmt(zC0_2) : "N/A (>2 anos)") + "</td>" +
          "<td>" + (isPretermActive ? getInfoPC(zC_Pre).faixa : is0_2 ? getInfoPC(zC0_2).faixa : "—") + "</td>" +
          "<td>" + (isPretermActive ? getInfoPC(zC_Pre).desc : is0_2 ? getInfoPC(zC0_2).desc : "Avaliação indicada até 24 meses") + "</td>" +
        "</tr>" +
      "</tbody>" +
    "</table>" +
    '<h4 style="margin-top:25px; margin-bottom:5px;">📈 Curvas de Crescimento da Caderneta</h4>' +
    '<h5 style="margin-top:15px; color:var(--text-muted);">1. Recém-Nascidos Pré-Termo (24 a 50 Semanas Pós-Concepcionais)</h5>' +
    '<div class="charts-grid">' +
      gerarSVG(tab, "peso_preterm", semanasPosConcepcional, peso, zP_Pre, getInfoPeso(zP_Pre), "Peso x Idade Pós-Concepcional", 24, 50, [24,28,32,36,40,44,48,50], isPretermActive, lblPreterm, sexo) +
      gerarSVG(tab, "est_preterm", semanasPosConcepcional, est, zE_Pre, getInfoEst(zE_Pre), "Comprimento x Idade Pós-Concepcional", 24, 50, [24,28,32,36,40,44,48,50], isPretermActive, lblPreterm, sexo) +
      gerarSVG(tab, "pc_preterm", semanasPosConcepcional, pc, zC_Pre, getInfoPC(zC_Pre), "Perímetro Cefálico x Idade Pós-Concepcional", 24, 50, [24,28,32,36,40,44,48,50], isPretermActive, lblPreterm, sexo) +
    '</div>' +
    '<h5 style="margin-top:25px; color:var(--text-muted);">2. Faixa Etária: 0 a 2 Anos (0 a 24 Meses Pós-Termo)</h5>' +
    '<div class="charts-grid">' +
      gerarSVG(tab, "peso_0_2", mInfantil, peso, zP0_2, getInfoPeso(zP0_2), "Peso x Idade (0-2a)", 0, 24, [0,3,6,9,12,15,18,21,24], is0_2, lbl0_2, sexo) +
      gerarSVG(tab, "est_0_2", mInfantil, est, zE0_2, getInfoEst(zE0_2), "Comprimento x Idade (0-2a)", 0, 24, [0,3,6,9,12,15,18,21,24], is0_2, lbl0_2, sexo) +
      gerarSVG(tab, "imc_0_2", mInfantil, imc, zI0_2, getInfoIMC(zI0_2), "IMC x Idade (0-2a)", 0, 24, [0,3,6,9,12,15,18,21,24], is0_2, lbl0_2, sexo) +
      gerarSVG(tab, "pc_0_2", mInfantil, pc, zC0_2, getInfoPC(zC0_2), "Perímetro Cefálico (0-2a)", 0, 24, [0,3,6,9,12,15,18,21,24], is0_2, lbl0_2, sexo) +
    '</div>' +
    '<h5 style="margin-top:25px; color:var(--text-muted);">3. Faixa Etária: 2 a 5 Anos (24 a 60 Meses)</h5>' +
    '<div class="charts-grid">' +
      gerarSVG(tab, "peso_2_5", mCrono, peso, zP2_5, getInfoPeso(zP2_5), "Peso x Idade (2-5a)", 24, 60, [24,30,36,42,48,54,60], is2_5, lbl2_5, sexo) +
      gerarSVG(tab, "est_2_5", mCrono, est, zE2_5, getInfoEst(zE2_5), "Estatura x Idade (2-5a)", 24, 60, [24,30,36,42,48,54,60], is2_5, lbl2_5, sexo) +
      gerarSVG(tab, "imc_2_5", mCrono, imc, zI2_5, getInfoIMC(zI2_5), "IMC x Idade (2-5a)", 24, 60, [24,30,36,42,48,54,60], is2_5, lbl2_5, sexo) +
    '</div>' +
    '<h5 style="margin-top:25px; color:var(--text-muted);">4. Faixa Etária: 5 a 10 Anos (60 a 120 Meses)</h5>' +
    '<div class="charts-grid">' +
      gerarSVG(tab, "peso_5_10", mCrono, peso, zP5_10, getInfoPeso(zP5_10), "Peso x Idade (5-10a)", 60, 120, [60,72,84,96,108,120], is5_10, lbl5_10, sexo) +
      gerarSVG(tab, "est_5_10", mCrono, est, zE5_10, getInfoEst(zE5_10), "Estatura x Idade (5-10a)", 60, 120, [60,72,84,96,108,120], is5_10, lbl5_10, sexo) +
      gerarSVG(tab, "imc_5_10", mCrono, imc, zI5_10, getInfoIMC(zI5_10), "IMC x Idade (5-10a)", 60, 120, [60,72,84,96,108,120], is5_10, lbl5_10, sexo) +
    '</div>';
});

$("calcular_dnpm").addEventListener("click", () => {
  const nasc = $("nasc").value;
  const data = $("data").value;
  const ig = $("ig").value === "" ? 40 : Number($("ig").value);

  if (!nasc || !data) {
    $("resultado_dnpm").textContent = "Por favor, preencha a data de nascimento no topo para realizar a avaliação do DNPM.";
    return;
  }

  let mCrono = idadeMeses(nasc, data);
  let semanasVida = diasEntre(nasc, data) / 7;
  let semanasPosConcepcional = ig + semanasVida;
  let descontoSemanas = 40 - ig;
  let mCorrig = mCrono - (descontoSemanas / 4.345);
  let mInfantil = (ig < 37 && mCorrig <= 24) ? mCorrig : mCrono;

  if (ig < 37 && semanasPosConcepcional < 40) {
    $("resultado_dnpm").innerHTML = 
      "<strong>Acompanhamento Neonatal de Pré-termo:</strong><br>" +
      "Idade Pós-Concepcional Atual: <strong>" + fmt(semanasPosConcepcional, 1) + " semanas</strong>.<br>" +
      "<em>* Criança ainda não atingiu a idade equivalente ao termo (40 semanas). Os marcos de desenvolvimento da Caderneta de Saúde da Criança são iniciados formalmente a partir de 0 a 1 mês de idade corrigida.</em>";
    return;
  }

  const faixaAtual = marcosDNPM.find(f => mInfantil >= f.min && mInfantil < f.max);

  if (!faixaAtual) {
    $("resultado_dnpm").innerHTML = "Idade de avaliação: <strong>" + fmt(mInfantil,1) + " meses</strong>. Fora da faixa de marcos rastreados da Caderneta (0 a 36 meses).";
    return;
  }

  const checkboxes = app.querySelectorAll('input[data-faixa="' + faixaAtual.id + '"]');
  let totalMarcos = 0;
  let marcadosNormais = 0;
  let alertasMarcados = 0;

  checkboxes.forEach(chk => {
    const isAlerta = chk.getAttribute("data-alerta") === "true";
    if (isAlerta) {
      if (chk.checked) alertasMarcados++;
    } else {
      totalMarcos++;
      if (chk.checked) marcadosNormais++;
    }
  });

  let statusHtml = "";
  if (alertasMarcados > 0) {
    statusHtml = '<span style="color:#e74c3c; font-weight:bold;">🚨 DESENVOLVIMENTO COM SINAL DE ALERTA / RISCO</span><br>Foi identificado pelo menos 1 sinal de risco/alerta importante para a faixa etária. Recomenda-se avaliação neurofuncional detalhada e encaminhamento especializado.';
  } else if (marcadosNormais === totalMarcos) {
    statusHtml = '<span style="color:#27ae60; font-weight:bold;">✅ DESENVOLVIMENTO ADEQUADO PARA A FAIXA ETÁRIA</span><br>A criança cumpre todos os marcos esperados para ' + faixaAtual.label + '. Manter estimulação em casa e orientações de puericultura.';
  } else if (marcadosNormais >= Math.ceil(totalMarcos / 2)) {
    statusHtml = '<span style="color:#f39c12; font-weight:bold;">⚠️ DESENVOLVIMENTO EM ALERTA (PARCIAL)</span><br>A criança apresenta alguns marcos esperados, mas faltam itens relevantes (' + marcadosNormais + '/' + totalMarcos + '). Orientar a família para reforçar estímulos e reavaliar em 30 dias.';
  } else {
    statusHtml = '<span style="color:#e74c3c; font-weight:bold;">🚨 PROVÁVEL ATRASO NO DESENVOLVIMENTO</span><br>Ausência da maioria dos marcos previstos para ' + faixaAtual.label + ' (' + marcadosNormais + '/' + totalMarcos + '). Necessário rastreio diagnóstico aprofundado e acompanhamento multidisciplinar.';
  }

  $("resultado_dnpm").innerHTML = 
    "<strong>Avaliação do DNPM (" + faixaAtual.label + "):</strong><br>" +
    "Idade de Referência: <strong>" + fmt(mInfantil, 1) + " meses</strong> " + (ig < 37 ? "(Idade Corrigida para Prematuro)" : "") + "<br><br>" +
    statusHtml;
});

$("validar_vacinas").addEventListener("click", () => {
  const nasc = $("nasc").value;
  const data = $("data").value;

  if (!nasc || !data) {
    $("resultado_vacinas").textContent = "Preencha a data de nascimento no topo para validar a carteira vacinal.";
    return;
  }

  let mCrono = idadeMeses(nasc, data);
  if (mCrono < 0) {
    $("resultado_vacinas").textContent = "A data da consulta não pode ser anterior ao nascimento.";
    return;
  }

  let vacinasEmAtraso = [];
  let vacinasTomadasCount = 0;
  let vacinasDevidasCount = 0;

  calendarioVacinas.forEach(p => {
    if (mCrono >= p.minMeses) {
      p.vacinas.forEach(v => {
        vacinasDevidasCount++;
        const chk = $("vac_" + v.id);
        if (chk && chk.checked) {
          vacinasTomadasCount++;
        } else {
          vacinasEmAtraso.push(v.nome + " (" + p.periodo + ")");
        }
      });
    }
  });

  let htmlRes = "";
  if (vacinasEmAtraso.length === 0) {
    htmlRes = '<span style="color:#27ae60; font-weight:bold;">✅ HISTÓRICO VACINAL ADEQUADO / EM DIA</span><br>' +
              'Todas as ' + vacinasDevidasCount + ' vacinas/doses previstas para a idade atual (' + fmt(mCrono, 1) + ' meses) foram devidamente administradas.';
  } else {
    htmlRes = '<span style="color:#e74c3c; font-weight:bold;">⚠️ HISTÓRICO VACINAL INADEQUADO / VACINAS EM ATRASO</span><br>' +
              'A criança possui <strong>' + vacinasEmAtraso.length + ' dose(s) pendente(s)</strong> para a idade atual (' + fmt(mCrono, 1) + ' meses):<br>' +
              '<ul style="margin-top:6px; margin-bottom:0; padding-left:20px;">' +
              vacinasEmAtraso.map(v => '<li>' + v + '</li>').join("") +
              '</ul>';
  }

  $("resultado_vacinas").innerHTML = htmlRes;
});

$("gerar_relatorio").addEventListener("click", () => {
  const nome = $("nome_paciente").value || "Paciente Pediátrico";
  const sexo = $("sexo").value === "M" ? "Masculino" : "Feminino";
  const nasc = $("nasc").value || "N/A";
  const data = $("data").value || "N/A";
  const ig = $("ig").value === "" ? 40 : Number($("ig").value);

  const peso = $("peso").value;
  const est = $("est").value;
  const pc = $("pc").value;
  const pa = $("pa").value;
  const pt = $("pt").value;

  const faStatus = $("fa_status").value;
  const faVal = $("fa_val").value;
  const faUnid = $("fa_unid").value;

  const fpStatus = $("fp_status").value;
  const fpVal = $("fp_val").value;
  const fpUnid = $("fp_unid").value;

  const fc = $("fc").value;
  const acDesc = $("ac_desc").value || "Sem alterações relatadas";

  const fr = $("fr").value;
  const apSel = $("ap_select").value;
  const apStr = apSel === "OUTRO" ? ($("ap_desc").value || "Sem alterações especificadas") : apSel;

  const otoSel = $("oto_select").value;
  const otoStr = otoSel === "OUTRO" ? ($("oto_outro").value || "Sem alterações especificadas") : otoSel;

  const rinoSel = $("rino_select").value;
  const rinoStr = rinoSel === "OUTRO" ? ($("rino_outro").value || "Sem alterações especificadas") : rinoSel;

  const oroSel = $("oro_select").value;
  const oroStr = oroSel === "OUTRO" ? ($("oro_outro").value || "Sem alterações especificadas") : oroSel;

  const genLivre = $("gen_desc_livre").value || "Sem alterações aparentes";

  let tannerStr = "";
  if (sexo === "Feminino") {
    tannerStr = "Mamas: " + $("tanner_m").value + " | Pelos Púbicos: " + $("tanner_pf").value;
  } else {
    tannerStr = "Genitália: " + $("tanner_g").value + " | Pelos Púbicos: " + $("tanner_pm").value;
  }

  let text = "AVALIAÇÃO DE PUERICULTURA E EXAME FÍSICO PEDIÁTRICO\n";
  text += "===================================================\n";
  text += "IDENTIFICAÇÃO:\n";
  text += "- Nome: " + nome + "\n";
  text += "- Sexo: " + sexo + " | Nascimento: " + nasc + " | Data Consulta: " + data + "\n";
  text += "- Idade Gestacional ao Nascer: " + ig + " semanas " + (ig < 37 ? "(Prematuro)" : "(A termo)") + "\n\n";

  text += "EXAME FÍSICO:\n";
  text += "1. Aparato Cardiovascular: FC = " + (fc ? fc + " bpm" : "N/I") + " | Ausculta: " + acDesc + "\n";
  text += "2. Aparato Respiratório: FR = " + (fr ? fr + " ipm" : "N/I") + " | Ausculta: " + apStr + "\n";
  text += "3. Otorrinolaringologia (ORL):\n";
  text += "   - Otoscopia: " + otoStr + "\n";
  text += "   - Rinoscopia: " + rinoStr + "\n";
  text += "   - Oroscopia: " + oroStr + "\n";
  text += "4. Genitália & Estadiamento Tanner:\n";
  text += "   - " + tannerStr + "\n";
  text += "   - Descrição Genital: " + genLivre + "\n\n";

  text += "AVALIAÇÃO DO DESENVOLVIMENTO (DNPM):\n";
  text += $("resultado_dnpm").innerText + "\n\n";

  text += "HISTÓRICO VACINAL:\n";
  text += $("resultado_vacinas").innerText + "\n\n";

  text += "ANTROPOMETRIA:\n";
  text += "- Peso: " + (peso ? peso + " kg" : "N/I") + " | Estatura: " + (est ? est + " cm" : "N/I") + "\n";
  text += "- Perímetro Cefálico: " + (pc ? pc + " cm" : "N/I") + "\n";
  text += "- Perímetro Abdominal: " + (pa ? pa + " cm" : "N/I") + " | Perímetro Torácico: " + (pt ? pt + " cm" : "N/I") + "\n";
  text += "- Fontanela Anterior: " + faStatus + (faVal ? " (" + faVal + " " + faUnid + ")" : "") + "\n";
  text += "- Fontanela Posterior: " + fpStatus + (fpVal ? " (" + fpVal + " " + fpUnid + ")" : "") + "\n";

  if (cacheUltimaAntropometria) {
    const c = cacheUltimaAntropometria;
    text += "\n  [Z-Scores Antropométricos Calculados]:\n";
    text += "  * Peso/Idade: Z = " + fmt(c.activeZ_P) + " (" + c.infoP.desc + ")\n";
    text += "  * Estatura/Idade: Z = " + fmt(c.activeZ_E) + " (" + c.infoE.desc + ")\n";
    text += "  * IMC/Idade: " + (c.isPretermActive ? "N/A (<40 semanas)" : "Z = " + fmt(c.activeZ_I) + " (" + c.infoI.desc + ")") + "\n";
    text += "  * PC/Idade: " + (c.zC != null ? "Z = " + fmt(c.zC) + " (" + c.infoC.desc + ")" : "N/A") + "\n";
  }
  text += "\n===================================================";

  $("box_relatorio").innerText = text;
});

$("copiar_relatorio").addEventListener("click", () => {
  const relatorioText = $("box_relatorio").innerText;
  if (!relatorioText || relatorioText.includes("Clique no botão acima")) {
    alert("Por favor, clique em 'Gerar Relatório Clínico Completo' antes de copiar.");
    return;
  }
  navigator.clipboard.writeText(relatorioText).then(() => {
    alert("Relatório copiado com sucesso para a Área de Transferência!");
  }).catch(() => {
    alert("Falha ao copiar automaticamente. Selecione o texto e copie manualmente.");
  });
});
```