# 👶 Prontuário Pediátrico Integrado com Puericultura, DNPM & Vacinação

```dataviewjs
// VERSÃO INTEGRADA E COMPLETA: Preserva 100% da interface e funcionalidades originais.
// Tabelas oficiais LMS da OMS incorporadas diretamente no código (funcionamento 100% offline):
// 1. Peso para Idade: OMS 0–120 meses (0 a 10 anos) - OMS Padrão 0-5a + OMS Referência 2007 5-10a.
// 2. Comprimento/Estatura para Idade: OMS 0–228 meses (0 a 19 anos) - Comprimento 0-24m + Estatura 24-60m e 61-228m (OMS 2007).
// 3. IMC para Idade: OMS 0–228 meses (0 a 19 anos) - Baseado em comprimento 0-24m + baseado em estatura 24-60m e 61-228m (OMS 2007).
// 4. Perímetro Cefálico para Idade: OMS 0–60 meses (0 a 5 anos).
// 5. Peso para Comprimento: OMS 45 a 110 cm (<24 meses).
// Metodologia OMS: ajuste de ±0,7 cm de posição (deitado vs em pé), correção de prematuridade (<37 sem) até 24 meses, ajuste de extremos >+3 e <-3 DP.
dv.container.innerHTML = "";

const wrapper = document.createElement("div");
wrapper.id = "pueri-full-app";

const style = document.createElement("style");
style.textContent = 
  "#pueri-full-app { font-family: var(--font-text); }" +
  "#pueri-full-app .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(145px, 1fr)); gap: 10px; }" +
  "#pueri-full-app .grid-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 10px; }" +
  "#pueri-full-app label { display: block; font-size: .85em; margin-bottom: 4px; font-weight: 600; }" +
  "#pueri-full-app input[type='text'], #pueri-full-app input[type='number'], #pueri-full-app input[type='date'], #pueri-full-app select, #pueri-full-app textarea { width: 100%; padding: 6px 10px; border: 1px solid var(--background-modifier-border); border-radius: 6px; background: var(--background-primary); color: var(--text-normal); box-sizing: border-box; font-family: inherit; }" +
  "#pueri-full-app textarea { height: 80px; resize: vertical; }" +
  "#pueri-full-app input[type='text'], #pueri-full-app input[type='number'], #pueri-full-app input[type='date'], #pueri-full-app select { height: 38px; }" +
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
    '<div style="grid-column: span 2;"><div id="idade_display" style="padding: 8px 12px; background: var(--background-secondary); border-radius: 6px; font-size: 0.9em; color: var(--text-muted); min-height: 38px; display: flex; align-items: center;">Preencha a data da consulta e data de nascimento para calcular a idade.</div></div>',
  '</div>',

  '<fieldset style="margin-top:15px;">',
    '<legend>Anamnese Inicial (HMA & HPP)</legend>',
    '<div style="margin-bottom:10px;"><label>História da Moléstia Atual (HMA)</label><textarea id="hma" placeholder="Descreva a queixa principal e evolução (suporta quebras de linha)..."></textarea></div>',
    '<div><label>História Patológica Pregressa (HPP)</label><textarea id="hpp" placeholder="Doenças prévias, internações, cirurgias, alergias (suporta quebras de linha)..."></textarea></div>',
  '</fieldset>',

  '<fieldset>',
    '<legend>Hábitos e Estilo de Vida</legend>',
    '<div class="grid-2" style="margin-bottom:10px;">',
      '<div><label>Alimentação (Lactente)</label><input id="hab_alimentacao" type="text" placeholder="Ex: Aleitamento materno exclusivo / Misto"></div>',
      '<div><label>Uso de Fórmula</label><input id="hab_formula" type="text" placeholder="Ex: Sim / Não / Qual marca"></div>',
    '</div>',
    '<div class="grid">',
      '<div><label>Hábito de Sono</label><input id="hab_sono" type="text" placeholder="Ex: Dorme bem, acorda 2x à noite"></div>',
      '<div><label>Trocas de Fralda</label><input id="hab_fraldas" type="text" placeholder="Ex: Frequência e aspecto habitual"></div>',
    '</div>',
  '</fieldset>',

  '<hr style="margin: 30px 0; border: 0; border-top: 2px solid var(--background-modifier-border);">',

  '<h3>2. Vigilância do Desenvolvimento Neuropsicomotor (DNPM)</h3>',
  '<div id="aviso_idade_dnpm" style="font-size:0.9em; margin-bottom:12px; color:var(--text-muted);">* O checklist da faixa etária atual será expandido automaticamente após o cálculo da antropometria.</div>',
  '<div id="dnpm_container"></div>',
  '<button id="calcular_dnpm">Avaliar Desenvolvimento (DNPM)</button>',
  '<div id="resultado_dnpm" class="resultado">Preencha os marcos do desenvolvimento e clique em avaliar.</div>',

  '<hr style="margin: 30px 0; border: 0; border-top: 2px solid var(--background-modifier-border);">',

  '<h3>3. Histórico & Carteira de Vacinação (PNI / Ministério da Saúde)</h3>',
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

  '<h3>4. Medidas Antropométricas & Ganho Ponderal</h3>',
  '<div class="grid">',
    '<div><label>Peso atual (kg)</label><input id="peso" type="number" min="0" step=".001"></div>',
    '<div><label>Comprimento/Estatura medida (cm)</label><input id="est" type="number" min="0" step=".1"></div>',
    '<div><label>Como a medida foi obtida?</label><select id="pos_est"><option value="deitado">Deitado (comprimento)</option><option value="em_pe">Em pé (estatura)</option></select><small>OMS: ajuste de 0,7 cm conforme idade e posição para usar a referência correta.</small></div>',
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
  '<div id="graficos_container" class="charts-grid"></div>',
  '<div id="recomendacoes_container"></div>',

  '<hr style="margin: 30px 0; border: 0; border-top: 2px solid var(--background-modifier-border);">',

  '<h3>5. Exame Físico Pediátrico Especializado</h3>',

  '<fieldset>',
    '<legend>Ausculta Cardiovascular</legend>',
    '<div class="grid-2">',
      '<div><label>Frequência Cardíaca (bpm)</label><input id="fc" type="number" placeholder="Ex: 120"></div>',
      '<div><label>Ausculta Cardíaca</label><select id="ac_select"><option value="BNF2T SS">BNF2T SS</option><option value="OUTRO">Outro (Descrever)</option></select></div>',
    '</div>',
    '<div id="ac_outro_div" style="margin-top:10px; display:none;"><label>Descrição da Ausculta Cardíaca</label><input id="ac_desc" type="text" placeholder="Descreva as alterações cardíacas..."></div>',
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

$("ac_select").addEventListener("change", (e) => {
  $("ac_outro_div").style.display = e.target.value === "OUTRO" ? "block" : "none";
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


const lmsOficial = {
  M: {
    peso: [[0,0.3487,3.3464,0.14602],[1,0.2297,4.4709,0.13395],[2,0.197,5.5675,0.12385],[3,0.1738,6.3762,0.11727],[4,0.1553,7.0023,0.11316],[5,0.1395,7.5105,0.1108],[6,0.1257,7.934,0.10958],[7,0.1134,8.297,0.10902],[8,0.1021,8.6151,0.10882],[9,0.0917,8.9014,0.10881],[10,0.082,9.1649,0.10891],[11,0.073,9.4122,0.10906],[12,0.0644,9.6479,0.10925],[13,0.0563,9.8749,0.10949],[14,0.0487,10.0953,0.10976],[15,0.0413,10.3108,0.11007],[16,0.0343,10.5228,0.11041],[17,0.0275,10.7319,0.11079],[18,0.0211,10.9385,0.11119],[19,0.0148,11.143,0.11164],[20,0.0087,11.3462,0.11211],[21,0.0029,11.5486,0.11261],[22,-0.0028,11.7504,0.11314],[23,-0.0083,11.9514,0.11369],[24,-0.0137,12.1515,0.11426],[25,-0.0189,12.3502,0.11485],[26,-0.024,12.5466,0.11544],[27,-0.0289,12.7401,0.11604],[28,-0.0337,12.9303,0.11664],[29,-0.0385,13.1169,0.11723],[30,-0.0431,13.3,0.11781],[31,-0.0476,13.4798,0.11839],[32,-0.052,13.6567,0.11896],[33,-0.0564,13.8309,0.11953],[34,-0.0606,14.0031,0.12008],[35,-0.0648,14.1736,0.12062],[36,-0.0689,14.3429,0.12116],[37,-0.0729,14.5113,0.12168],[38,-0.0769,14.6791,0.1222],[39,-0.0808,14.8466,0.12271],[40,-0.0846,15.014,0.12322],[41,-0.0883,15.1813,0.12373],[42,-0.092,15.3486,0.12425],[43,-0.0957,15.5158,0.12478],[44,-0.0993,15.6828,0.12531],[45,-0.1028,15.8497,0.12586],[46,-0.1063,16.0163,0.12643],[47,-0.1097,16.1827,0.127],[48,-0.1131,16.3489,0.12759],[49,-0.1165,16.515,0.12819],[50,-0.1198,16.6811,0.1288],[51,-0.123,16.8471,0.12943],[52,-0.1262,17.0132,0.13005],[53,-0.1294,17.1792,0.13069],[54,-0.1325,17.3452,0.13133],[55,-0.1356,17.5111,0.13197],[56,-0.1387,17.6768,0.13261],[57,-0.1417,17.8422,0.13325],[58,-0.1447,18.0073,0.13389],[59,-0.1477,18.1722,0.13453],[60,-0.1506,18.3366,0.13517],[61,-0.2026,18.5057,0.12988],[62,-0.213,18.6802,0.13028],[63,-0.2234,18.8563,0.13067],[64,-0.2338,19.034,0.13105],[65,-0.2443,19.2132,0.13142],[66,-0.2548,19.394,0.13178],[67,-0.2653,19.5765,0.13213],[68,-0.2758,19.7607,0.13246],[69,-0.2864,19.9468,0.13279],[70,-0.2969,20.1344,0.13311],[71,-0.3075,20.3235,0.13342],[72,-0.318,20.5137,0.13372],[73,-0.3285,20.7052,0.13402],[74,-0.339,20.8979,0.13432],[75,-0.3494,21.0918,0.13462],[76,-0.3598,21.287,0.13493],[77,-0.3701,21.4833,0.13523],[78,-0.3804,21.681,0.13554],[79,-0.3906,21.8799,0.13586],[80,-0.4007,22.08,0.13618],[81,-0.4107,22.2813,0.13652],[82,-0.4207,22.4837,0.13686],[83,-0.4305,22.6872,0.13722],[84,-0.4402,22.8915,0.13759],[85,-0.4499,23.0968,0.13797],[86,-0.4594,23.3029,0.13838],[87,-0.4688,23.5101,0.1388],[88,-0.4781,23.7182,0.13923],[89,-0.4873,23.9272,0.13969],[90,-0.4964,24.1371,0.14016],[91,-0.5053,24.3479,0.14065],[92,-0.5142,24.5595,0.14117],[93,-0.5229,24.7722,0.1417],[94,-0.5315,24.9858,0.14226],[95,-0.5399,25.2005,0.14284],[96,-0.5482,25.4163,0.14344],[97,-0.5564,25.6332,0.14407],[98,-0.5644,25.8513,0.14472],[99,-0.5722,26.0706,0.14539],[100,-0.5799,26.2911,0.14608],[101,-0.5873,26.5128,0.14679],[102,-0.5946,26.7358,0.14752],[103,-0.6017,26.9602,0.14828],[104,-0.6085,27.1861,0.14905],[105,-0.6152,27.4137,0.14984],[106,-0.6216,27.6432,0.15066],[107,-0.6278,27.875,0.15149],[108,-0.6337,28.1092,0.15233],[109,-0.6393,28.3459,0.15319],[110,-0.6446,28.5854,0.15406],[111,-0.6496,28.8277,0.15493],[112,-0.6543,29.0731,0.15581],[113,-0.6585,29.3217,0.1567],[114,-0.6624,29.5736,0.1576],[115,-0.6659,29.8289,0.1585],[116,-0.6689,30.0877,0.1594],[117,-0.6714,30.3501,0.16031],[118,-0.6735,30.616,0.16122],[119,-0.6752,30.8854,0.16213],[120,-0.6764,31.1586,0.16305]],
    comp: [[0,1,49.8842,0.03795],[1,1,54.7244,0.03557],[2,1,58.4249,0.03424],[3,1,61.4292,0.03328],[4,1,63.886,0.03257],[5,1,65.9026,0.03204],[6,1,67.6236,0.03165],[7,1,69.1645,0.03139],[8,1,70.5994,0.03124],[9,1,71.9687,0.03117],[10,1,73.2812,0.03118],[11,1,74.5388,0.03125],[12,1,75.7488,0.03137],[13,1,76.9186,0.03154],[14,1,78.0497,0.03174],[15,1,79.1458,0.03197],[16,1,80.2113,0.03222],[17,1,81.2487,0.0325],[18,1,82.2587,0.03279],[19,1,83.2418,0.0331],[20,1,84.1996,0.03342],[21,1,85.1348,0.03376],[22,1,86.0477,0.0341],[23,1,86.941,0.03445],[24,1,87.8161,0.03479]],
    est: [[24,1,87.1161,0.03507],[25,1,87.972,0.03542],[26,1,88.8065,0.03576],[27,1,89.6197,0.0361],[28,1,90.412,0.03642],[29,1,91.1828,0.03674],[30,1,91.9327,0.03704],[31,1,92.6631,0.03733],[32,1,93.3753,0.03761],[33,1,94.0711,0.03787],[34,1,94.7532,0.03812],[35,1,95.4236,0.03836],[36,1,96.0835,0.03858],[37,1,96.7337,0.03879],[38,1,97.3749,0.039],[39,1,98.0073,0.03919],[40,1,98.631,0.03937],[41,1,99.2459,0.03954],[42,1,99.8515,0.03971],[43,1,100.4485,0.03986],[44,1,101.0374,0.04002],[45,1,101.6186,0.04016],[46,1,102.1933,0.04031],[47,1,102.7625,0.04045],[48,1,103.3273,0.04059],[49,1,103.8886,0.04073],[50,1,104.4473,0.04086],[51,1,105.0041,0.041],[52,1,105.5596,0.04113],[53,1,106.1138,0.04126],[54,1,106.6668,0.04139],[55,1,107.2188,0.04152],[56,1,107.7697,0.04165],[57,1,108.3198,0.04177],[58,1,108.8689,0.0419],[59,1,109.417,0.04202],[60,1,109.9638,0.04214],[61,1,110.2647,0.04164],[62,1,110.8006,0.04172],[63,1,111.3338,0.0418],[64,1,111.8636,0.04187],[65,1,112.3895,0.04195],[66,1,112.911,0.04203],[67,1,113.428,0.04211],[68,1,113.941,0.04218],[69,1,114.45,0.04226],[70,1,114.9547,0.04234],[71,1,115.4549,0.04241],[72,1,115.9509,0.04249],[73,1,116.4432,0.04257],[74,1,116.9325,0.04264],[75,1,117.4196,0.04272],[76,1,117.9046,0.0428],[77,1,118.388,0.04287],[78,1,118.87,0.04295],[79,1,119.3508,0.04303],[80,1,119.8303,0.04311],[81,1,120.3085,0.04318],[82,1,120.7853,0.04326],[83,1,121.2604,0.04334],[84,1,121.7338,0.04342],[85,1,122.2053,0.0435],[86,1,122.675,0.04358],[87,1,123.1429,0.04366],[88,1,123.6092,0.04374],[89,1,124.0736,0.04382],[90,1,124.5361,0.0439],[91,1,124.9964,0.04398],[92,1,125.4545,0.04406],[93,1,125.9104,0.04414],[94,1,126.364,0.04422],[95,1,126.8156,0.0443],[96,1,127.2651,0.04438],[97,1,127.7129,0.04446],[98,1,128.159,0.04454],[99,1,128.6034,0.04462],[100,1,129.0466,0.0447],[101,1,129.4887,0.04478],[102,1,129.93,0.04487],[103,1,130.3705,0.04495],[104,1,130.8103,0.04503],[105,1,131.2495,0.04511],[106,1,131.6884,0.04519],[107,1,132.1269,0.04527],[108,1,132.5652,0.04535],[109,1,133.0031,0.04543],[110,1,133.4404,0.04551],[111,1,133.877,0.04559],[112,1,134.313,0.04566],[113,1,134.7483,0.04574],[114,1,135.1829,0.04582],[115,1,135.6168,0.04589],[116,1,136.0501,0.04597],[117,1,136.4829,0.04604],[118,1,136.9153,0.04612],[119,1,137.3474,0.04619],[120,1,137.7795,0.04626],[121,1,138.2119,0.04633],[122,1,138.6452,0.0464],[123,1,139.0797,0.04647],[124,1,139.5158,0.04654],[125,1,139.954,0.04661],[126,1,140.3948,0.04667],[127,1,140.8387,0.04674],[128,1,141.2859,0.0468],[129,1,141.7368,0.04686],[130,1,142.1916,0.04692],[131,1,142.6501,0.04698],[132,1,143.1126,0.04703],[133,1,143.5795,0.04709],[134,1,144.0511,0.04714],[135,1,144.5276,0.04719],[136,1,145.0093,0.04723],[137,1,145.4964,0.04728],[138,1,145.9891,0.04732],[139,1,146.4878,0.04736],[140,1,146.9927,0.0474],[141,1,147.5041,0.04744],[142,1,148.0224,0.04747],[143,1,148.5478,0.0475],[144,1,149.0807,0.04753],[145,1,149.6212,0.04755],[146,1,150.1694,0.04758],[147,1,150.7256,0.04759],[148,1,151.2899,0.04761],[149,1,151.8623,0.04762],[150,1,152.4425,0.04763],[151,1,153.0298,0.04763],[152,1,153.6234,0.04764],[153,1,154.2223,0.04763],[154,1,154.8258,0.04763],[155,1,155.4329,0.04762],[156,1,156.0426,0.0476],[157,1,156.6539,0.04758],[158,1,157.266,0.04756],[159,1,157.8775,0.04754],[160,1,158.4871,0.04751],[161,1,159.0937,0.04747],[162,1,159.6962,0.04744],[163,1,160.2939,0.0474],[164,1,160.8861,0.04735],[165,1,161.472,0.0473],[166,1,162.0505,0.04725],[167,1,162.6207,0.0472],[168,1,163.1816,0.04714],[169,1,163.7321,0.04707],[170,1,164.2717,0.04701],[171,1,164.7994,0.04694],[172,1,165.3145,0.04687],[173,1,165.8165,0.04679],[174,1,166.305,0.04671],[175,1,166.7799,0.04663],[176,1,167.2415,0.04655],[177,1,167.6899,0.04646],[178,1,168.1255,0.04637],[179,1,168.5482,0.04628],[180,1,168.958,0.04619],[181,1,169.3549,0.04609],[182,1,169.7389,0.04599],[183,1,170.1099,0.04589],[184,1,170.468,0.04579],[185,1,170.8136,0.04569],[186,1,171.1468,0.04559],[187,1,171.468,0.04548],[188,1,171.7773,0.04538],[189,1,172.0748,0.04527],[190,1,172.3606,0.04516],[191,1,172.6345,0.04506],[192,1,172.8967,0.04495],[193,1,173.147,0.04484],[194,1,173.3856,0.04473],[195,1,173.6126,0.04462],[196,1,173.828,0.04451],[197,1,174.0321,0.0444],[198,1,174.2251,0.04429],[199,1,174.4071,0.04418],[200,1,174.5784,0.04407],[201,1,174.7392,0.04396],[202,1,174.8896,0.04385],[203,1,175.0301,0.04375],[204,1,175.1609,0.04364],[205,1,175.2824,0.04353],[206,1,175.3951,0.04343],[207,1,175.4995,0.04332],[208,1,175.5959,0.04322],[209,1,175.685,0.04311],[210,1,175.7672,0.04301],[211,1,175.8432,0.04291],[212,1,175.9133,0.04281],[213,1,175.9781,0.04271],[214,1,176.038,0.04261],[215,1,176.0935,0.04251],[216,1,176.1449,0.04241],[217,1,176.1925,0.04232],[218,1,176.2368,0.04222],[219,1,176.2779,0.04213],[220,1,176.3162,0.04204],[221,1,176.3518,0.04195],[222,1,176.3851,0.04185],[223,1,176.4162,0.04177],[224,1,176.4453,0.04168],[225,1,176.4724,0.04159],[226,1,176.4976,0.0415],[227,1,176.5211,0.04142],[228,1,176.5432,0.04134]],
    pc: [[0,1,34.4618,0.03686],[1,1,37.2759,0.03133],[2,1,39.1285,0.02997],[3,1,40.5135,0.02918],[4,1,41.6317,0.02868],[5,1,42.5576,0.02837],[6,1,43.3306,0.02817],[7,1,43.9803,0.02804],[8,1,44.53,0.02796],[9,1,44.9998,0.02792],[10,1,45.4051,0.0279],[11,1,45.7573,0.02789],[12,1,46.0661,0.02789],[13,1,46.3395,0.02789],[14,1,46.5844,0.02791],[15,1,46.806,0.02792],[16,1,47.0088,0.02795],[17,1,47.1962,0.02797],[18,1,47.3711,0.028],[19,1,47.5357,0.02803],[20,1,47.6919,0.02806],[21,1,47.8408,0.0281],[22,1,47.9833,0.02813],[23,1,48.1201,0.02817],[24,1,48.2515,0.02821],[25,1,48.3777,0.02825],[26,1,48.4989,0.0283],[27,1,48.6151,0.02834],[28,1,48.7264,0.02838],[29,1,48.8331,0.02842],[30,1,48.9351,0.02847],[31,1,49.0327,0.02851],[32,1,49.126,0.02855],[33,1,49.2153,0.02859],[34,1,49.3007,0.02863],[35,1,49.3826,0.02867],[36,1,49.4612,0.02871],[37,1,49.5367,0.02875],[38,1,49.6093,0.02878],[39,1,49.6791,0.02882],[40,1,49.7465,0.02886],[41,1,49.8116,0.02889],[42,1,49.8745,0.02893],[43,1,49.9354,0.02896],[44,1,49.9942,0.02899],[45,1,50.0512,0.02903],[46,1,50.1064,0.02906],[47,1,50.1598,0.02909],[48,1,50.2115,0.02912],[49,1,50.2617,0.02915],[50,1,50.3105,0.02918],[51,1,50.3578,0.02921],[52,1,50.4039,0.02924],[53,1,50.4488,0.02927],[54,1,50.4926,0.02929],[55,1,50.5354,0.02932],[56,1,50.5772,0.02935],[57,1,50.6183,0.02938],[58,1,50.6587,0.0294],[59,1,50.6984,0.02943],[60,1,50.7375,0.02946]],
    imcL: [[0,-0.3053,13.4069,0.0956],[1,0.2708,14.9441,0.09027],[2,0.1118,16.3195,0.08677],[3,0.0068,16.8987,0.08495],[4,-0.0727,17.1579,0.08378],[5,-0.137,17.2919,0.08296],[6,-0.1913,17.3422,0.08234],[7,-0.2385,17.3288,0.08183],[8,-0.2802,17.2647,0.0814],[9,-0.3176,17.1662,0.08102],[10,-0.3516,17.0488,0.08068],[11,-0.3828,16.9239,0.08037],[12,-0.4115,16.7981,0.08009],[13,-0.4382,16.6743,0.07982],[14,-0.463,16.5548,0.07958],[15,-0.4863,16.4409,0.07935],[16,-0.5082,16.3335,0.07913],[17,-0.5289,16.2329,0.07892],[18,-0.5484,16.1392,0.07873],[19,-0.5669,16.0528,0.07854],[20,-0.5846,15.9743,0.07836],[21,-0.6014,15.9039,0.07818],[22,-0.6174,15.8412,0.07802],[23,-0.6328,15.7852,0.07786],[24,-0.6473,15.7356,0.07771]],
    imcH: [[24,-0.6187,16.0189,0.07785],[25,-0.584,15.98,0.07792],[26,-0.5497,15.9414,0.078],[27,-0.5166,15.9036,0.07808],[28,-0.485,15.8667,0.07818],[29,-0.4552,15.8306,0.07829],[30,-0.4274,15.7953,0.07841],[31,-0.4016,15.7606,0.07854],[32,-0.3782,15.7267,0.07867],[33,-0.3572,15.6934,0.07882],[34,-0.3388,15.661,0.07897],[35,-0.3231,15.6294,0.07914],[36,-0.3101,15.5988,0.07931],[37,-0.3,15.5693,0.0795],[38,-0.2927,15.541,0.07969],[39,-0.2884,15.514,0.0799],[40,-0.2869,15.4885,0.08012],[41,-0.2881,15.4645,0.08036],[42,-0.2919,15.442,0.08061],[43,-0.2981,15.421,0.08087],[44,-0.3067,15.4013,0.08115],[45,-0.3174,15.3827,0.08144],[46,-0.3303,15.3652,0.08174],[47,-0.3452,15.3485,0.08205],[48,-0.3622,15.3326,0.08238],[49,-0.3811,15.3174,0.08272],[50,-0.4019,15.3029,0.08307],[51,-0.4245,15.2891,0.08343],[52,-0.4488,15.2759,0.0838],[53,-0.4747,15.2633,0.08418],[54,-0.5019,15.2514,0.08457],[55,-0.5303,15.24,0.08496],[56,-0.5599,15.2291,0.08536],[57,-0.5905,15.2188,0.08577],[58,-0.6223,15.2091,0.08617],[59,-0.6552,15.2,0.08659],[60,-0.6892,15.1916,0.087],[61,-0.7387,15.2641,0.0839],[62,-0.7621,15.2616,0.08414],[63,-0.7856,15.2604,0.08439],[64,-0.8089,15.2605,0.08464],[65,-0.8322,15.2619,0.0849],[66,-0.8554,15.2645,0.08516],[67,-0.8785,15.2684,0.08543],[68,-0.9015,15.2737,0.0857],[69,-0.9243,15.2801,0.08597],[70,-0.9471,15.2877,0.08625],[71,-0.9697,15.2965,0.08653],[72,-0.9921,15.3062,0.08682],[73,-1.0144,15.3169,0.08711],[74,-1.0365,15.3285,0.08741],[75,-1.0584,15.3408,0.08771],[76,-1.0801,15.354,0.08802],[77,-1.1017,15.3679,0.08833],[78,-1.123,15.3825,0.08865],[79,-1.1441,15.3978,0.08898],[80,-1.1649,15.4137,0.08931],[81,-1.1856,15.4302,0.08964],[82,-1.206,15.4473,0.08998],[83,-1.2261,15.465,0.09033],[84,-1.246,15.4832,0.09068],[85,-1.2656,15.5019,0.09103],[86,-1.2849,15.521,0.09139],[87,-1.304,15.5407,0.09176],[88,-1.3228,15.5608,0.09213],[89,-1.3414,15.5814,0.09251],[90,-1.3596,15.6023,0.09289],[91,-1.3776,15.6237,0.09327],[92,-1.3953,15.6455,0.09366],[93,-1.4126,15.6677,0.09406],[94,-1.4297,15.6903,0.09445],[95,-1.4464,15.7133,0.09486],[96,-1.4629,15.7368,0.09526],[97,-1.479,15.7606,0.09567],[98,-1.4947,15.7848,0.09609],[99,-1.5101,15.8094,0.09651],[100,-1.5252,15.8344,0.09693],[101,-1.5399,15.8597,0.09735],[102,-1.5542,15.8855,0.09778],[103,-1.5681,15.9116,0.09821],[104,-1.5817,15.9381,0.09864],[105,-1.5948,15.9651,0.09907],[106,-1.6076,15.9925,0.09951],[107,-1.6199,16.0205,0.09994],[108,-1.6318,16.049,0.10038],[109,-1.6433,16.0781,0.10082],[110,-1.6544,16.1078,0.10126],[111,-1.6651,16.1381,0.1017],[112,-1.6753,16.1692,0.10214],[113,-1.6851,16.2009,0.10259],[114,-1.6944,16.2333,0.10303],[115,-1.7032,16.2665,0.10347],[116,-1.7116,16.3004,0.10391],[117,-1.7196,16.3351,0.10435],[118,-1.7271,16.3704,0.10478],[119,-1.7341,16.4065,0.10522],[120,-1.7407,16.4433,0.10566],[121,-1.7468,16.4807,0.10609],[122,-1.7525,16.5189,0.10652],[123,-1.7578,16.5578,0.10695],[124,-1.7626,16.5974,0.10738],[125,-1.767,16.6376,0.1078],[126,-1.771,16.6786,0.10823],[127,-1.7745,16.7203,0.10865],[128,-1.7777,16.7628,0.10906],[129,-1.7804,16.8059,0.10948],[130,-1.7828,16.8497,0.10989],[131,-1.7847,16.8941,0.1103],[132,-1.7862,16.9392,0.1107],[133,-1.7873,16.985,0.1111],[134,-1.7881,17.0314,0.1115],[135,-1.7884,17.0784,0.11189],[136,-1.7884,17.1262,0.11228],[137,-1.788,17.1746,0.11266],[138,-1.7873,17.2236,0.11304],[139,-1.7861,17.2734,0.11342],[140,-1.7846,17.324,0.11379],[141,-1.7828,17.3752,0.11415],[142,-1.7806,17.4272,0.11451],[143,-1.778,17.4799,0.11487],[144,-1.7751,17.5334,0.11522],[145,-1.7719,17.5877,0.11556],[146,-1.7684,17.6427,0.1159],[147,-1.7645,17.6985,0.11623],[148,-1.7604,17.7551,0.11656],[149,-1.7559,17.8124,0.11688],[150,-1.7511,17.8704,0.1172],[151,-1.7461,17.9292,0.11751],[152,-1.7408,17.9887,0.11781],[153,-1.7352,18.0488,0.11811],[154,-1.7293,18.1096,0.11841],[155,-1.7232,18.171,0.11869],[156,-1.7168,18.233,0.11898],[157,-1.7102,18.2955,0.11925],[158,-1.7033,18.3586,0.11952],[159,-1.6962,18.4221,0.11979],[160,-1.6888,18.486,0.12005],[161,-1.6811,18.5502,0.1203],[162,-1.6732,18.6148,0.12055],[163,-1.6651,18.6795,0.12079],[164,-1.6568,18.7445,0.12102],[165,-1.6482,18.8095,0.12125],[166,-1.6394,18.8746,0.12148],[167,-1.6304,18.9398,0.1217],[168,-1.6211,19.005,0.12191],[169,-1.6116,19.0701,0.12212],[170,-1.602,19.1351,0.12233],[171,-1.5921,19.2,0.12253],[172,-1.5821,19.2648,0.12272],[173,-1.5719,19.3294,0.12291],[174,-1.5615,19.3937,0.1231],[175,-1.551,19.4578,0.12328],[176,-1.5403,19.5217,0.12346],[177,-1.5294,19.5853,0.12363],[178,-1.5185,19.6486,0.1238],[179,-1.5074,19.7117,0.12396],[180,-1.4961,19.7744,0.12412],[181,-1.4848,19.8367,0.12428],[182,-1.4733,19.8987,0.12443],[183,-1.4617,19.9603,0.12458],[184,-1.45,20.0215,0.12473],[185,-1.4382,20.0823,0.12487],[186,-1.4263,20.1427,0.12501],[187,-1.4143,20.2026,0.12514],[188,-1.4022,20.2621,0.12528],[189,-1.39,20.3211,0.12541],[190,-1.3777,20.3796,0.12554],[191,-1.3653,20.4376,0.12567],[192,-1.3529,20.4951,0.12579],[193,-1.3403,20.5521,0.12591],[194,-1.3277,20.6085,0.12603],[195,-1.3149,20.6644,0.12615],[196,-1.3021,20.7197,0.12627],[197,-1.2892,20.7745,0.12638],[198,-1.2762,20.8287,0.1265],[199,-1.2631,20.8824,0.12661],[200,-1.2499,20.9355,0.12672],[201,-1.2366,20.9881,0.12683],[202,-1.2233,21.04,0.12694],[203,-1.2098,21.0914,0.12704],[204,-1.1962,21.1423,0.12715],[205,-1.1826,21.1925,0.12726],[206,-1.1688,21.2423,0.12736],[207,-1.155,21.2914,0.12746],[208,-1.141,21.34,0.12756],[209,-1.127,21.388,0.12767],[210,-1.1129,21.4354,0.12777],[211,-1.0986,21.4822,0.12787],[212,-1.0843,21.5285,0.12797],[213,-1.0699,21.5742,0.12807],[214,-1.0553,21.6193,0.12816],[215,-1.0407,21.6638,0.12826],[216,-1.026,21.7077,0.12836],[217,-1.0112,21.751,0.12845],[218,-0.9962,21.7937,0.12855],[219,-0.9812,21.8358,0.12864],[220,-0.9661,21.8773,0.12874],[221,-0.9509,21.9182,0.12883],[222,-0.9356,21.9585,0.12893],[223,-0.9202,21.9982,0.12902],[224,-0.9048,22.0374,0.12911],[225,-0.8892,22.076,0.1292],[226,-0.8735,22.114,0.1293],[227,-0.8578,22.1514,0.12939],[228,-0.8419,22.1883,0.12948]],
    pesoComprimento: [[45,-0.3521,2.441,0.09182],[45.5,-0.3521,2.5244,0.09153],[46,-0.3521,2.6077,0.09124],[46.5,-0.3521,2.6913,0.09094],[47,-0.3521,2.7755,0.09065],[47.5,-0.3521,2.8609,0.09036],[48,-0.3521,2.948,0.09007],[48.5,-0.3521,3.0377,0.08977],[49,-0.3521,3.1308,0.08948],[49.5,-0.3521,3.2276,0.08919],[50,-0.3521,3.3278,0.0889],[50.5,-0.3521,3.4311,0.08861],[51,-0.3521,3.5376,0.08831],[51.5,-0.3521,3.6477,0.08801],[52,-0.3521,3.762,0.08771],[52.5,-0.3521,3.8814,0.08741],[53,-0.3521,4.006,0.08711],[53.5,-0.3521,4.1354,0.08681],[54,-0.3521,4.2693,0.08651],[54.5,-0.3521,4.4066,0.08621],[55,-0.3521,4.5467,0.08592],[55.5,-0.3521,4.6892,0.08563],[56,-0.3521,4.8338,0.08535],[56.5,-0.3521,4.9796,0.08507],[57,-0.3521,5.1259,0.08481],[57.5,-0.3521,5.2721,0.08455],[58,-0.3521,5.418,0.0843],[58.5,-0.3521,5.5632,0.08406],[59,-0.3521,5.7074,0.08383],[59.5,-0.3521,5.8501,0.08362],[60,-0.3521,5.9907,0.08342],[60.5,-0.3521,6.1284,0.08324],[61,-0.3521,6.2632,0.08308],[61.5,-0.3521,6.3954,0.08292],[62,-0.3521,6.5251,0.08279],[62.5,-0.3521,6.6527,0.08266],[63,-0.3521,6.7786,0.08255],[63.5,-0.3521,6.9028,0.08245],[64,-0.3521,7.0255,0.08236],[64.5,-0.3521,7.1467,0.08229],[65,-0.3521,7.2666,0.08223],[65.5,-0.3521,7.3854,0.08218],[66,-0.3521,7.5034,0.08215],[66.5,-0.3521,7.6206,0.08213],[67,-0.3521,7.737,0.08212],[67.5,-0.3521,7.8526,0.08212],[68,-0.3521,7.9674,0.08214],[68.5,-0.3521,8.0816,0.08216],[69,-0.3521,8.1955,0.08219],[69.5,-0.3521,8.3092,0.08224],[70,-0.3521,8.4227,0.08229],[70.5,-0.3521,8.5358,0.08235],[71,-0.3521,8.648,0.08241],[71.5,-0.3521,8.7594,0.08248],[72,-0.3521,8.8697,0.08254],[72.5,-0.3521,8.9788,0.08262],[73,-0.3521,9.0865,0.08269],[73.5,-0.3521,9.1927,0.08276],[74,-0.3521,9.2974,0.08283],[74.5,-0.3521,9.401,0.08289],[75,-0.3521,9.5032,0.08295],[75.5,-0.3521,9.6041,0.08301],[76,-0.3521,9.7033,0.08307],[76.5,-0.3521,9.8007,0.08311],[77,-0.3521,9.8963,0.08314],[77.5,-0.3521,9.9902,0.08317],[78,-0.3521,10.0827,0.08318],[78.5,-0.3521,10.1741,0.08318],[79,-0.3521,10.2649,0.08316],[79.5,-0.3521,10.3558,0.08313],[80,-0.3521,10.4475,0.08308],[80.5,-0.3521,10.5405,0.08301],[81,-0.3521,10.6352,0.08293],[81.5,-0.3521,10.7322,0.08284],[82,-0.3521,10.8321,0.08273],[82.5,-0.3521,10.935,0.0826],[83,-0.3521,11.0415,0.08246],[83.5,-0.3521,11.1516,0.08231],[84,-0.3521,11.2651,0.08215],[84.5,-0.3521,11.3817,0.08198],[85,-0.3521,11.5007,0.08181],[85.5,-0.3521,11.6218,0.08163],[86,-0.3521,11.7444,0.08145],[86.5,-0.3521,11.8678,0.08128],[87,-0.3521,11.9916,0.08111],[87.5,-0.3521,12.1152,0.08096],[88,-0.3521,12.2382,0.08082],[88.5,-0.3521,12.3603,0.08069],[89,-0.3521,12.4815,0.08058],[89.5,-0.3521,12.6017,0.08048],[90,-0.3521,12.7209,0.08041],[90.5,-0.3521,12.8392,0.08034],[91,-0.3521,12.9569,0.0803],[91.5,-0.3521,13.0742,0.08026],[92,-0.3521,13.191,0.08025],[92.5,-0.3521,13.3075,0.08025],[93,-0.3521,13.4239,0.08026],[93.5,-0.3521,13.5404,0.08029],[94,-0.3521,13.6572,0.08034],[94.5,-0.3521,13.7746,0.0804],[95,-0.3521,13.8928,0.08047],[95.5,-0.3521,14.012,0.08056],[96,-0.3521,14.1325,0.08067],[96.5,-0.3521,14.2544,0.08078],[97,-0.3521,14.3782,0.08092],[97.5,-0.3521,14.5038,0.08106],[98,-0.3521,14.6316,0.08122],[98.5,-0.3521,14.7614,0.08139],[99,-0.3521,14.8934,0.08157],[99.5,-0.3521,15.0275,0.08177],[100,-0.3521,15.1637,0.08198],[100.5,-0.3521,15.3018,0.0822],[101,-0.3521,15.4419,0.08243],[101.5,-0.3521,15.5838,0.08267],[102,-0.3521,15.7276,0.08292],[102.5,-0.3521,15.8732,0.08317],[103,-0.3521,16.0206,0.08343],[103.5,-0.3521,16.1697,0.0837],[104,-0.3521,16.3204,0.08397],[104.5,-0.3521,16.4728,0.08425],[105,-0.3521,16.6268,0.08453],[105.5,-0.3521,16.7826,0.08481],[106,-0.3521,16.9401,0.0851],[106.5,-0.3521,17.0995,0.08539],[107,-0.3521,17.2607,0.08568],[107.5,-0.3521,17.4237,0.08599],[108,-0.3521,17.5885,0.08629],[108.5,-0.3521,17.7553,0.0866],[109,-0.3521,17.9242,0.08691],[109.5,-0.3521,18.0954,0.08723],[110,-0.3521,18.2689,0.08755]]
  },
  F: {
    peso: [[0,0.3809,3.2322,0.14171],[1,0.1714,4.1873,0.13724],[2,0.0962,5.1282,0.13],[3,0.0402,5.8458,0.12619],[4,-0.005,6.4237,0.12402],[5,-0.043,6.8985,0.12274],[6,-0.0756,7.297,0.12204],[7,-0.1039,7.6422,0.12178],[8,-0.1288,7.9487,0.12181],[9,-0.1507,8.2254,0.12199],[10,-0.17,8.48,0.12223],[11,-0.1872,8.7192,0.12247],[12,-0.2024,8.9481,0.12268],[13,-0.2158,9.1699,0.12283],[14,-0.2278,9.387,0.12294],[15,-0.2384,9.6008,0.12299],[16,-0.2478,9.8124,0.12303],[17,-0.2562,10.0226,0.12306],[18,-0.2637,10.2315,0.12309],[19,-0.2703,10.4393,0.12315],[20,-0.2762,10.6464,0.12323],[21,-0.2815,10.8534,0.12335],[22,-0.2862,11.0608,0.1235],[23,-0.2903,11.2688,0.12369],[24,-0.2941,11.4775,0.1239],[25,-0.2975,11.6864,0.12414],[26,-0.3005,11.8947,0.12441],[27,-0.3032,12.1015,0.12472],[28,-0.3057,12.3059,0.12506],[29,-0.308,12.5073,0.12545],[30,-0.3101,12.7055,0.12587],[31,-0.312,12.9006,0.12633],[32,-0.3138,13.093,0.12683],[33,-0.3155,13.2837,0.12737],[34,-0.3171,13.4731,0.12794],[35,-0.3186,13.6618,0.12855],[36,-0.3201,13.8503,0.12919],[37,-0.3216,14.0385,0.12988],[38,-0.323,14.2265,0.13059],[39,-0.3243,14.414,0.13135],[40,-0.3257,14.601,0.13213],[41,-0.327,14.7873,0.13293],[42,-0.3283,14.9727,0.13376],[43,-0.3296,15.1573,0.1346],[44,-0.3309,15.341,0.13545],[45,-0.3322,15.524,0.1363],[46,-0.3335,15.7064,0.13716],[47,-0.3348,15.8882,0.138],[48,-0.3361,16.0697,0.13884],[49,-0.3374,16.2511,0.13968],[50,-0.3387,16.4322,0.14051],[51,-0.34,16.6133,0.14132],[52,-0.3414,16.7942,0.14213],[53,-0.3427,16.9748,0.14293],[54,-0.344,17.1551,0.14371],[55,-0.3453,17.3347,0.14448],[56,-0.3466,17.5136,0.14525],[57,-0.3479,17.6916,0.146],[58,-0.3492,17.8686,0.14675],[59,-0.3505,18.0445,0.14748],[60,-0.3518,18.2193,0.14821],[61,-0.4681,18.2579,0.14295],[62,-0.4711,18.4329,0.1435],[63,-0.4742,18.6073,0.14404],[64,-0.4773,18.7811,0.14459],[65,-0.4803,18.9545,0.14514],[66,-0.4834,19.1276,0.14569],[67,-0.4864,19.3004,0.14624],[68,-0.4894,19.473,0.14679],[69,-0.4924,19.6455,0.14735],[70,-0.4954,19.818,0.1479],[71,-0.4984,19.9908,0.14845],[72,-0.5013,20.1639,0.149],[73,-0.5043,20.3377,0.14955],[74,-0.5072,20.5124,0.1501],[75,-0.51,20.6885,0.15065],[76,-0.5129,20.8661,0.1512],[77,-0.5157,21.0457,0.15175],[78,-0.5185,21.2274,0.1523],[79,-0.5213,21.4113,0.15284],[80,-0.524,21.5979,0.15339],[81,-0.5268,21.7872,0.15393],[82,-0.5294,21.9795,0.15448],[83,-0.5321,22.1751,0.15502],[84,-0.5347,22.374,0.15556],[85,-0.5372,22.5762,0.1561],[86,-0.5398,22.7816,0.15663],[87,-0.5423,22.9904,0.15717],[88,-0.5447,23.2025,0.1577],[89,-0.5471,23.418,0.15823],[90,-0.5495,23.6369,0.15876],[91,-0.5518,23.8593,0.15928],[92,-0.5541,24.0853,0.1598],[93,-0.5563,24.3149,0.16032],[94,-0.5585,24.5482,0.16084],[95,-0.5606,24.7853,0.16135],[96,-0.5627,25.0262,0.16186],[97,-0.5647,25.271,0.16237],[98,-0.5667,25.5197,0.16287],[99,-0.5686,25.7721,0.16337],[100,-0.5704,26.0284,0.16386],[101,-0.5722,26.2883,0.16435],[102,-0.574,26.5519,0.16483],[103,-0.5757,26.819,0.16532],[104,-0.5773,27.0896,0.16579],[105,-0.5789,27.3635,0.16626],[106,-0.5804,27.6406,0.16673],[107,-0.5819,27.9208,0.16719],[108,-0.5833,28.204,0.16764],[109,-0.5847,28.4901,0.16809],[110,-0.5859,28.7791,0.16854],[111,-0.5872,29.0711,0.16897],[112,-0.5883,29.3663,0.16941],[113,-0.5895,29.6646,0.16983],[114,-0.5905,29.9663,0.17025],[115,-0.5915,30.2715,0.17066],[116,-0.5925,30.5805,0.17107],[117,-0.5934,30.8934,0.17146],[118,-0.5942,31.2105,0.17186],[119,-0.595,31.5319,0.17224],[120,-0.5958,31.8578,0.17262]],
    comp: [[0,1,49.1477,0.0379],[1,1,53.6872,0.0364],[2,1,57.0673,0.03568],[3,1,59.8029,0.0352],[4,1,62.0899,0.03486],[5,1,64.0301,0.03463],[6,1,65.7311,0.03448],[7,1,67.2873,0.03441],[8,1,68.7498,0.0344],[9,1,70.1435,0.03444],[10,1,71.4818,0.03452],[11,1,72.771,0.03464],[12,1,74.015,0.03479],[13,1,75.2176,0.03496],[14,1,76.3817,0.03514],[15,1,77.5099,0.03534],[16,1,78.6055,0.03555],[17,1,79.671,0.03576],[18,1,80.7079,0.03598],[19,1,81.7182,0.0362],[20,1,82.7036,0.03643],[21,1,83.6654,0.03666],[22,1,84.604,0.03688],[23,1,85.5202,0.03711],[24,1,86.4153,0.03734]],
    est: [[24,1,85.7153,0.03764],[25,1,86.5904,0.03786],[26,1,87.4462,0.03808],[27,1,88.283,0.0383],[28,1,89.1004,0.03851],[29,1,89.8991,0.03872],[30,1,90.6797,0.03893],[31,1,91.443,0.03913],[32,1,92.1906,0.03933],[33,1,92.9239,0.03952],[34,1,93.6444,0.03971],[35,1,94.3533,0.03989],[36,1,95.0515,0.04006],[37,1,95.7399,0.04024],[38,1,96.4187,0.04041],[39,1,97.0885,0.04057],[40,1,97.7493,0.04073],[41,1,98.4015,0.04089],[42,1,99.0448,0.04105],[43,1,99.6795,0.0412],[44,1,100.3058,0.04135],[45,1,100.9238,0.0415],[46,1,101.5337,0.04164],[47,1,102.136,0.04179],[48,1,102.7312,0.04193],[49,1,103.3197,0.04206],[50,1,103.9021,0.0422],[51,1,104.4786,0.04233],[52,1,105.0494,0.04246],[53,1,105.6148,0.04259],[54,1,106.1748,0.04272],[55,1,106.7295,0.04285],[56,1,107.2788,0.04298],[57,1,107.8227,0.0431],[58,1,108.3613,0.04322],[59,1,108.8948,0.04334],[60,1,109.4233,0.04347],[61,1,109.6016,0.04355],[62,1,110.1258,0.04364],[63,1,110.6451,0.04373],[64,1,111.1596,0.04382],[65,1,111.6696,0.0439],[66,1,112.1753,0.04399],[67,1,112.6767,0.04407],[68,1,113.174,0.04415],[69,1,113.6672,0.04423],[70,1,114.1565,0.04431],[71,1,114.6421,0.04439],[72,1,115.1244,0.04447],[73,1,115.6039,0.04454],[74,1,116.0812,0.04461],[75,1,116.5568,0.04469],[76,1,117.0311,0.04475],[77,1,117.5044,0.04482],[78,1,117.9769,0.04489],[79,1,118.4489,0.04495],[80,1,118.9208,0.04502],[81,1,119.3926,0.04508],[82,1,119.8648,0.04514],[83,1,120.3374,0.0452],[84,1,120.8105,0.04525],[85,1,121.2843,0.04531],[86,1,121.7587,0.04536],[87,1,122.2338,0.04542],[88,1,122.7098,0.04547],[89,1,123.1868,0.04551],[90,1,123.6646,0.04556],[91,1,124.1435,0.04561],[92,1,124.6234,0.04565],[93,1,125.1045,0.04569],[94,1,125.5869,0.04573],[95,1,126.0706,0.04577],[96,1,126.5558,0.04581],[97,1,127.0424,0.04585],[98,1,127.5304,0.04588],[99,1,128.0199,0.04591],[100,1,128.5109,0.04594],[101,1,129.0035,0.04597],[102,1,129.4975,0.046],[103,1,129.9932,0.04602],[104,1,130.4904,0.04604],[105,1,130.9891,0.04607],[106,1,131.4895,0.04608],[107,1,131.9912,0.0461],[108,1,132.4944,0.04612],[109,1,132.9989,0.04613],[110,1,133.5046,0.04614],[111,1,134.0118,0.04615],[112,1,134.5202,0.04616],[113,1,135.0299,0.04616],[114,1,135.541,0.04617],[115,1,136.0533,0.04617],[116,1,136.567,0.04616],[117,1,137.0821,0.04616],[118,1,137.5987,0.04616],[119,1,138.1167,0.04615],[120,1,138.6363,0.04614],[121,1,139.1575,0.04612],[122,1,139.6803,0.04611],[123,1,140.2049,0.04609],[124,1,140.7313,0.04607],[125,1,141.2594,0.04605],[126,1,141.7892,0.04603],[127,1,142.3206,0.046],[128,1,142.8534,0.04597],[129,1,143.3874,0.04594],[130,1,143.9222,0.04591],[131,1,144.4575,0.04588],[132,1,144.9929,0.04584],[133,1,145.528,0.0458],[134,1,146.0622,0.04576],[135,1,146.5951,0.04571],[136,1,147.1262,0.04567],[137,1,147.6548,0.04562],[138,1,148.1804,0.04557],[139,1,148.7023,0.04552],[140,1,149.2197,0.04546],[141,1,149.7322,0.04541],[142,1,150.239,0.04535],[143,1,150.7394,0.04529],[144,1,151.2327,0.04523],[145,1,151.7182,0.04516],[146,1,152.1951,0.0451],[147,1,152.6628,0.04503],[148,1,153.1206,0.04497],[149,1,153.5678,0.0449],[150,1,154.0041,0.04483],[151,1,154.429,0.04476],[152,1,154.8423,0.04468],[153,1,155.2437,0.04461],[154,1,155.633,0.04454],[155,1,156.0101,0.04446],[156,1,156.3748,0.04439],[157,1,156.7269,0.04431],[158,1,157.0666,0.04423],[159,1,157.3936,0.04415],[160,1,157.7082,0.04408],[161,1,158.0102,0.044],[162,1,158.2997,0.04392],[163,1,158.5771,0.04384],[164,1,158.8425,0.04376],[165,1,159.0961,0.04369],[166,1,159.3382,0.04361],[167,1,159.5691,0.04353],[168,1,159.789,0.04345],[169,1,159.9983,0.04337],[170,1,160.1971,0.0433],[171,1,160.3857,0.04322],[172,1,160.5643,0.04314],[173,1,160.7332,0.04307],[174,1,160.8927,0.04299],[175,1,161.043,0.04292],[176,1,161.1845,0.04284],[177,1,161.3176,0.04277],[178,1,161.4425,0.0427],[179,1,161.5596,0.04263],[180,1,161.6692,0.04255],[181,1,161.7717,0.04248],[182,1,161.8673,0.04241],[183,1,161.9564,0.04235],[184,1,162.0393,0.04228],[185,1,162.1164,0.04221],[186,1,162.188,0.04214],[187,1,162.2542,0.04208],[188,1,162.3154,0.04201],[189,1,162.3719,0.04195],[190,1,162.4239,0.04189],[191,1,162.4717,0.04182],[192,1,162.5156,0.04176],[193,1,162.556,0.0417],[194,1,162.5933,0.04164],[195,1,162.6276,0.04158],[196,1,162.6594,0.04152],[197,1,162.689,0.04147],[198,1,162.7165,0.04141],[199,1,162.7425,0.04136],[200,1,162.767,0.0413],[201,1,162.7904,0.04125],[202,1,162.8126,0.04119],[203,1,162.834,0.04114],[204,1,162.8545,0.04109],[205,1,162.8743,0.04104],[206,1,162.8935,0.04099],[207,1,162.912,0.04094],[208,1,162.93,0.04089],[209,1,162.9476,0.04084],[210,1,162.9649,0.0408],[211,1,162.9817,0.04075],[212,1,162.9983,0.04071],[213,1,163.0144,0.04066],[214,1,163.03,0.04062],[215,1,163.0451,0.04058],[216,1,163.0595,0.04053],[217,1,163.0733,0.04049],[218,1,163.0862,0.04045],[219,1,163.0982,0.04041],[220,1,163.1092,0.04037],[221,1,163.1192,0.04034],[222,1,163.1279,0.0403],[223,1,163.1355,0.04026],[224,1,163.1418,0.04023],[225,1,163.1469,0.04019],[226,1,163.1508,0.04016],[227,1,163.1534,0.04012],[228,1,163.1548,0.04009]],
    pc: [[0,1,33.8787,0.03496],[1,1,36.5463,0.0321],[2,1,38.2521,0.03168],[3,1,39.5328,0.0314],[4,1,40.5817,0.03119],[5,1,41.459,0.03102],[6,1,42.1995,0.03087],[7,1,42.829,0.03075],[8,1,43.3671,0.03063],[9,1,43.83,0.03053],[10,1,44.2319,0.03044],[11,1,44.5844,0.03035],[12,1,44.8965,0.03027],[13,1,45.1752,0.03019],[14,1,45.4265,0.03012],[15,1,45.6551,0.03006],[16,1,45.865,0.02999],[17,1,46.0598,0.02993],[18,1,46.2424,0.02987],[19,1,46.4152,0.02982],[20,1,46.5801,0.02977],[21,1,46.7384,0.02972],[22,1,46.8913,0.02967],[23,1,47.0391,0.02962],[24,1,47.1822,0.02957],[25,1,47.3204,0.02953],[26,1,47.4536,0.02949],[27,1,47.5817,0.02945],[28,1,47.7045,0.02941],[29,1,47.8219,0.02937],[30,1,47.934,0.02933],[31,1,48.041,0.02929],[32,1,48.1432,0.02926],[33,1,48.2408,0.02922],[34,1,48.3343,0.02919],[35,1,48.4239,0.02915],[36,1,48.5099,0.02912],[37,1,48.5926,0.02909],[38,1,48.6722,0.02906],[39,1,48.7489,0.02903],[40,1,48.8228,0.029],[41,1,48.8941,0.02897],[42,1,48.9629,0.02894],[43,1,49.0294,0.02891],[44,1,49.0937,0.02888],[45,1,49.156,0.02886],[46,1,49.2164,0.02883],[47,1,49.2751,0.0288],[48,1,49.3321,0.02878],[49,1,49.3877,0.02875],[50,1,49.4419,0.02873],[51,1,49.4947,0.0287],[52,1,49.5464,0.02868],[53,1,49.5969,0.02865],[54,1,49.6464,0.02863],[55,1,49.6947,0.02861],[56,1,49.7421,0.02859],[57,1,49.7885,0.02856],[58,1,49.8341,0.02854],[59,1,49.8789,0.02852],[60,1,49.9229,0.0285]],
    imcL: [[0,-0.0631,13.3363,0.09272],[1,0.3448,14.5679,0.09556],[2,0.1749,15.7679,0.09371],[3,0.0643,16.3574,0.09254],[4,-0.0191,16.6703,0.09166],[5,-0.0864,16.8386,0.09096],[6,-0.1429,16.9083,0.09036],[7,-0.1916,16.902,0.08984],[8,-0.2344,16.8404,0.08939],[9,-0.2725,16.7406,0.08898],[10,-0.3068,16.6184,0.08861],[11,-0.3381,16.4875,0.08828],[12,-0.3667,16.3568,0.08797],[13,-0.3932,16.2311,0.08768],[14,-0.4177,16.1128,0.08741],[15,-0.4407,16.0028,0.08716],[16,-0.4623,15.9017,0.08693],[17,-0.4825,15.8096,0.08671],[18,-0.5017,15.7263,0.0865],[19,-0.5199,15.6517,0.0863],[20,-0.5372,15.5855,0.08612],[21,-0.5537,15.5278,0.08594],[22,-0.5695,15.4787,0.08577],[23,-0.5846,15.438,0.0856],[24,-0.5989,15.4052,0.08545]],
    imcH: [[24,-0.5684,15.6881,0.08454],[25,-0.5684,15.659,0.08452],[26,-0.5684,15.6308,0.08449],[27,-0.5684,15.6037,0.08446],[28,-0.5684,15.5777,0.08444],[29,-0.5684,15.5523,0.08443],[30,-0.5684,15.5276,0.08444],[31,-0.5684,15.5034,0.08448],[32,-0.5684,15.4798,0.08455],[33,-0.5684,15.4572,0.08467],[34,-0.5684,15.4356,0.08484],[35,-0.5684,15.4155,0.08506],[36,-0.5684,15.3968,0.08535],[37,-0.5684,15.3796,0.08569],[38,-0.5684,15.3638,0.08609],[39,-0.5684,15.3493,0.08654],[40,-0.5684,15.3358,0.08704],[41,-0.5684,15.3233,0.08757],[42,-0.5684,15.3116,0.08813],[43,-0.5684,15.3007,0.08872],[44,-0.5684,15.2905,0.08931],[45,-0.5684,15.2814,0.08991],[46,-0.5684,15.2732,0.09051],[47,-0.5684,15.2661,0.0911],[48,-0.5684,15.2602,0.09168],[49,-0.5684,15.2556,0.09227],[50,-0.5684,15.2523,0.09286],[51,-0.5684,15.2503,0.09345],[52,-0.5684,15.2496,0.09403],[53,-0.5684,15.2502,0.0946],[54,-0.5684,15.2519,0.09515],[55,-0.5684,15.2544,0.09568],[56,-0.5684,15.2575,0.09618],[57,-0.5684,15.2612,0.09665],[58,-0.5684,15.2653,0.09709],[59,-0.5684,15.2698,0.0975],[60,-0.5684,15.2747,0.09789],[61,-0.8886,15.2441,0.09692],[62,-0.9068,15.2434,0.09738],[63,-0.9248,15.2433,0.09783],[64,-0.9427,15.2438,0.09829],[65,-0.9605,15.2448,0.09875],[66,-0.978,15.2464,0.0992],[67,-0.9954,15.2487,0.09966],[68,-1.0126,15.2516,0.10012],[69,-1.0296,15.2551,0.10058],[70,-1.0464,15.2592,0.10104],[71,-1.063,15.2641,0.10149],[72,-1.0794,15.2697,0.10195],[73,-1.0956,15.276,0.10241],[74,-1.1115,15.2831,0.10287],[75,-1.1272,15.2911,0.10333],[76,-1.1427,15.2998,0.10379],[77,-1.1579,15.3095,0.10425],[78,-1.1728,15.32,0.10471],[79,-1.1875,15.3314,0.10517],[80,-1.2019,15.3439,0.10562],[81,-1.216,15.3572,0.10608],[82,-1.2298,15.3717,0.10654],[83,-1.2433,15.3871,0.107],[84,-1.2565,15.4036,0.10746],[85,-1.2693,15.4211,0.10792],[86,-1.2819,15.4397,0.10837],[87,-1.2941,15.4593,0.10883],[88,-1.306,15.4798,0.10929],[89,-1.3175,15.5014,0.10974],[90,-1.3287,15.524,0.1102],[91,-1.3395,15.5476,0.11065],[92,-1.3499,15.5723,0.1111],[93,-1.36,15.5979,0.11156],[94,-1.3697,15.6246,0.11201],[95,-1.379,15.6523,0.11246],[96,-1.388,15.681,0.11291],[97,-1.3966,15.7107,0.11335],[98,-1.4047,15.7415,0.1138],[99,-1.4125,15.7732,0.11424],[100,-1.4199,15.8058,0.11469],[101,-1.427,15.8394,0.11513],[102,-1.4336,15.8738,0.11557],[103,-1.4398,15.909,0.11601],[104,-1.4456,15.9451,0.11644],[105,-1.4511,15.9818,0.11688],[106,-1.4561,16.0194,0.11731],[107,-1.4607,16.0575,0.11774],[108,-1.465,16.0964,0.11816],[109,-1.4688,16.1358,0.11859],[110,-1.4723,16.1759,0.11901],[111,-1.4753,16.2166,0.11943],[112,-1.478,16.258,0.11985],[113,-1.4803,16.2999,0.12026],[114,-1.4823,16.3425,0.12067],[115,-1.4838,16.3858,0.12108],[116,-1.485,16.4298,0.12148],[117,-1.4859,16.4746,0.12188],[118,-1.4864,16.52,0.12228],[119,-1.4866,16.5663,0.12268],[120,-1.4864,16.6133,0.12307],[121,-1.4859,16.6612,0.12346],[122,-1.4851,16.71,0.12384],[123,-1.4839,16.7595,0.12422],[124,-1.4825,16.81,0.1246],[125,-1.4807,16.8614,0.12497],[126,-1.4787,16.9136,0.12534],[127,-1.4763,16.9667,0.12571],[128,-1.4737,17.0208,0.12607],[129,-1.4708,17.0757,0.12643],[130,-1.4677,17.1316,0.12678],[131,-1.4642,17.1883,0.12713],[132,-1.4606,17.2459,0.12748],[133,-1.4567,17.3044,0.12782],[134,-1.4526,17.3637,0.12816],[135,-1.4482,17.4238,0.12849],[136,-1.4436,17.4847,0.12882],[137,-1.4389,17.5464,0.12914],[138,-1.4339,17.6088,0.12946],[139,-1.4288,17.6719,0.12978],[140,-1.4235,17.7357,0.13009],[141,-1.418,17.8001,0.1304],[142,-1.4123,17.8651,0.1307],[143,-1.4065,17.9306,0.13099],[144,-1.4006,17.9966,0.13129],[145,-1.3945,18.063,0.13158],[146,-1.3883,18.1297,0.13186],[147,-1.3819,18.1967,0.13214],[148,-1.3755,18.2639,0.13241],[149,-1.3689,18.3312,0.13268],[150,-1.3621,18.3986,0.13295],[151,-1.3553,18.466,0.13321],[152,-1.3483,18.5333,0.13347],[153,-1.3413,18.6006,0.13372],[154,-1.3341,18.6677,0.13397],[155,-1.3269,18.7346,0.13421],[156,-1.3195,18.8012,0.13445],[157,-1.3121,18.8675,0.13469],[158,-1.3046,18.9335,0.13492],[159,-1.297,18.9991,0.13514],[160,-1.2894,19.0642,0.13537],[161,-1.2816,19.1289,0.13559],[162,-1.2739,19.1931,0.1358],[163,-1.2661,19.2567,0.13601],[164,-1.2583,19.3197,0.13622],[165,-1.2504,19.382,0.13642],[166,-1.2425,19.4437,0.13662],[167,-1.2345,19.5045,0.13681],[168,-1.2266,19.5647,0.137],[169,-1.2186,19.624,0.13719],[170,-1.2107,19.6824,0.13738],[171,-1.2027,19.74,0.13756],[172,-1.1947,19.7966,0.13774],[173,-1.1867,19.8523,0.13791],[174,-1.1788,19.907,0.13808],[175,-1.1708,19.9607,0.13825],[176,-1.1629,20.0133,0.13841],[177,-1.1549,20.0648,0.13858],[178,-1.147,20.1152,0.13873],[179,-1.139,20.1644,0.13889],[180,-1.1311,20.2125,0.13904],[181,-1.1232,20.2595,0.1392],[182,-1.1153,20.3053,0.13934],[183,-1.1074,20.3499,0.13949],[184,-1.0996,20.3934,0.13963],[185,-1.0917,20.4357,0.13977],[186,-1.0838,20.4769,0.13991],[187,-1.076,20.517,0.14005],[188,-1.0681,20.556,0.14018],[189,-1.0603,20.5938,0.14031],[190,-1.0525,20.6306,0.14044],[191,-1.0447,20.6663,0.14057],[192,-1.0368,20.7008,0.1407],[193,-1.029,20.7344,0.14082],[194,-1.0212,20.7668,0.14094],[195,-1.0134,20.7982,0.14106],[196,-1.0055,20.8286,0.14118],[197,-0.9977,20.858,0.1413],[198,-0.9898,20.8863,0.14142],[199,-0.9819,20.9137,0.14153],[200,-0.974,20.9401,0.14164],[201,-0.9661,20.9656,0.14176],[202,-0.9582,20.9901,0.14187],[203,-0.9503,21.0138,0.14198],[204,-0.9423,21.0367,0.14208],[205,-0.9344,21.0587,0.14219],[206,-0.9264,21.0801,0.1423],[207,-0.9184,21.1007,0.1424],[208,-0.9104,21.1206,0.1425],[209,-0.9024,21.1399,0.14261],[210,-0.8944,21.1586,0.14271],[211,-0.8863,21.1768,0.14281],[212,-0.8783,21.1944,0.14291],[213,-0.8703,21.2116,0.14301],[214,-0.8623,21.2282,0.14311],[215,-0.8542,21.2444,0.1432],[216,-0.8462,21.2603,0.1433],[217,-0.8382,21.2757,0.1434],[218,-0.8301,21.2908,0.14349],[219,-0.8221,21.3055,0.14359],[220,-0.814,21.32,0.14368],[221,-0.806,21.3341,0.14377],[222,-0.798,21.348,0.14386],[223,-0.7899,21.3617,0.14396],[224,-0.7819,21.3752,0.14405],[225,-0.7738,21.3884,0.14414],[226,-0.7658,21.4014,0.14423],[227,-0.7577,21.4143,0.14432],[228,-0.7496,21.4269,0.14441]],
    pesoComprimento: [[45,-0.3833,2.4607,0.09029],[45.5,-0.3833,2.5457,0.09033],[46,-0.3833,2.6306,0.09037],[46.5,-0.3833,2.7155,0.0904],[47,-0.3833,2.8007,0.09044],[47.5,-0.3833,2.8867,0.09048],[48,-0.3833,2.9741,0.09052],[48.5,-0.3833,3.0636,0.09056],[49,-0.3833,3.156,0.0906],[49.5,-0.3833,3.252,0.09064],[50,-0.3833,3.3518,0.09068],[50.5,-0.3833,3.4557,0.09072],[51,-0.3833,3.5636,0.09076],[51.5,-0.3833,3.6754,0.0908],[52,-0.3833,3.7911,0.09085],[52.5,-0.3833,3.9105,0.09089],[53,-0.3833,4.0332,0.09093],[53.5,-0.3833,4.1591,0.09098],[54,-0.3833,4.2875,0.09102],[54.5,-0.3833,4.4179,0.09106],[55,-0.3833,4.5498,0.0911],[55.5,-0.3833,4.6827,0.09114],[56,-0.3833,4.8162,0.09118],[56.5,-0.3833,4.95,0.09121],[57,-0.3833,5.0837,0.09125],[57.5,-0.3833,5.2173,0.09128],[58,-0.3833,5.3507,0.0913],[58.5,-0.3833,5.4834,0.09132],[59,-0.3833,5.6151,0.09134],[59.5,-0.3833,5.7454,0.09135],[60,-0.3833,5.8742,0.09136],[60.5,-0.3833,6.0014,0.09137],[61,-0.3833,6.127,0.09137],[61.5,-0.3833,6.2511,0.09136],[62,-0.3833,6.3738,0.09135],[62.5,-0.3833,6.4948,0.09133],[63,-0.3833,6.6144,0.09131],[63.5,-0.3833,6.7328,0.09129],[64,-0.3833,6.8501,0.09126],[64.5,-0.3833,6.9662,0.09123],[65,-0.3833,7.0812,0.09119],[65.5,-0.3833,7.195,0.09115],[66,-0.3833,7.3076,0.0911],[66.5,-0.3833,7.4189,0.09106],[67,-0.3833,7.5288,0.09101],[67.5,-0.3833,7.6375,0.09096],[68,-0.3833,7.7448,0.0909],[68.5,-0.3833,7.8509,0.09085],[69,-0.3833,7.9559,0.09079],[69.5,-0.3833,8.0599,0.09074],[70,-0.3833,8.163,0.09068],[70.5,-0.3833,8.2651,0.09062],[71,-0.3833,8.3666,0.09056],[71.5,-0.3833,8.4676,0.0905],[72,-0.3833,8.5679,0.09043],[72.5,-0.3833,8.6674,0.09037],[73,-0.3833,8.7661,0.09031],[73.5,-0.3833,8.8638,0.09025],[74,-0.3833,8.9601,0.09018],[74.5,-0.3833,9.0552,0.09012],[75,-0.3833,9.149,0.09005],[75.5,-0.3833,9.2418,0.08999],[76,-0.3833,9.3337,0.08992],[76.5,-0.3833,9.4252,0.08985],[77,-0.3833,9.5166,0.08979],[77.5,-0.3833,9.6086,0.08972],[78,-0.3833,9.7015,0.08965],[78.5,-0.3833,9.7957,0.08959],[79,-0.3833,9.8915,0.08952],[79.5,-0.3833,9.9892,0.08946],[80,-0.3833,10.0891,0.0894],[80.5,-0.3833,10.1916,0.08934],[81,-0.3833,10.2965,0.08928],[81.5,-0.3833,10.4041,0.08923],[82,-0.3833,10.514,0.08918],[82.5,-0.3833,10.6263,0.08914],[83,-0.3833,10.741,0.0891],[83.5,-0.3833,10.8578,0.08906],[84,-0.3833,10.9767,0.08903],[84.5,-0.3833,11.0974,0.089],[85,-0.3833,11.2198,0.08898],[85.5,-0.3833,11.3435,0.08897],[86,-0.3833,11.4684,0.08895],[86.5,-0.3833,11.594,0.08895],[87,-0.3833,11.7201,0.08895],[87.5,-0.3833,11.8461,0.08895],[88,-0.3833,11.972,0.08896],[88.5,-0.3833,12.0976,0.08898],[89,-0.3833,12.2229,0.089],[89.5,-0.3833,12.3477,0.08903],[90,-0.3833,12.4723,0.08906],[90.5,-0.3833,12.5965,0.08909],[91,-0.3833,12.7205,0.08913],[91.5,-0.3833,12.8443,0.08918],[92,-0.3833,12.9681,0.08923],[92.5,-0.3833,13.092,0.08928],[93,-0.3833,13.2158,0.08934],[93.5,-0.3833,13.3399,0.08941],[94,-0.3833,13.4643,0.08948],[94.5,-0.3833,13.5892,0.08955],[95,-0.3833,13.7146,0.08963],[95.5,-0.3833,13.8408,0.08972],[96,-0.3833,13.9676,0.08981],[96.5,-0.3833,14.0953,0.0899],[97,-0.3833,14.2239,0.09],[97.5,-0.3833,14.3537,0.0901],[98,-0.3833,14.4848,0.09021],[98.5,-0.3833,14.6174,0.09033],[99,-0.3833,14.7519,0.09044],[99.5,-0.3833,14.8882,0.09057],[100,-0.3833,15.0267,0.09069],[100.5,-0.3833,15.1676,0.09083],[101,-0.3833,15.3108,0.09096],[101.5,-0.3833,15.4564,0.0911],[102,-0.3833,15.6046,0.09125],[102.5,-0.3833,15.7553,0.09139],[103,-0.3833,15.9087,0.09155],[103.5,-0.3833,16.0645,0.0917],[104,-0.3833,16.2229,0.09186],[104.5,-0.3833,16.3837,0.09203],[105,-0.3833,16.547,0.09219],[105.5,-0.3833,16.7129,0.09236],[106,-0.3833,16.8814,0.09254],[106.5,-0.3833,17.0527,0.09271],[107,-0.3833,17.2269,0.09289],[107.5,-0.3833,17.4039,0.09307],[108,-0.3833,17.5839,0.09326],[108.5,-0.3833,17.7668,0.09344],[109,-0.3833,17.9526,0.09363],[109.5,-0.3833,18.1412,0.09382],[110,-0.3833,18.3324,0.09401]]
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
  { id: "v_0", periodo: "Ao Nascer", minMeses: 0, maxMeses: 2, vacinas: [
      { id: "bcg", nome: "BCG (Dose única)" },
      { id: "hepb_0", nome: "Hepatite B (Dose ao nascer)" }
    ]
  },
  { id: "v_2", periodo: "2 Meses", minMeses: 2, maxMeses: 3, vacinas: [
      { id: "penta_1", nome: "Pentavalente (1ª dose)" },
      { id: "vip_1", nome: "VIP / Polio Inativada (1ª dose)" },
      { id: "pneumo_1", nome: "Pneumocócica 10V (1ª dose)" },
      { id: "rota_1", nome: "Rotavírus Humano VRH (1ª dose)" }
    ]
  },
  { id: "v_3", periodo: "3 Meses", minMeses: 3, maxMeses: 4, vacinas: [
      { id: "meningo_1", nome: "Meningocócica C (1ª dose)" }
    ]
  },
  { id: "v_4", periodo: "4 Meses", minMeses: 4, maxMeses: 5, vacinas: [
      { id: "penta_2", nome: "Pentavalente (2ª dose)" },
      { id: "vip_2", nome: "VIP / Polio Inativada (2ª dose)" },
      { id: "pneumo_2", nome: "Pneumocócica 10V (2ª dose)" },
      { id: "rota_2", nome: "Rotavírus Humano VRH (2ª dose)" }
    ]
  },
  { id: "v_5", periodo: "5 Meses", minMeses: 5, maxMeses: 6, vacinas: [
      { id: "meningo_2", nome: "Meningocócica C (2ª dose)" }
    ]
  },
  { id: "v_6", periodo: "6 Meses", minMeses: 6, maxMeses: 7, vacinas: [
      { id: "penta_3", nome: "Pentavalente (3ª dose)" },
      { id: "vip_3", nome: "VIP / Polio Inativada (3ª dose)" },
      { id: "covid_1", nome: "COVID-19 (1ª dose)" }
    ]
  },
  { id: "v_7", periodo: "7 a 9 Meses", minMeses: 7, maxMeses: 12, vacinas: [
      { id: "covid_2", nome: "COVID-19 (2ª dose)" },
      { id: "fa_1", nome: "Febre Amarela (1ª dose aos 9m)" }
    ]
  },
  { id: "v_12", periodo: "12 Meses (1 Ano)", minMeses: 12, maxMeses: 15, vacinas: [
      { id: "triplice_1", nome: "Tríplice Viral - SCR (1ª dose)" },
      { id: "pneumo_ref", nome: "Pneumocócica 10V (Reforço)" },
      { id: "meningo_ref", nome: "Meningocócica C (Reforço)" }
    ]
  },
  { id: "v_15", periodo: "15 Meses", minMeses: 15, maxMeses: 48, vacinas: [
      { id: "dtp_ref1", nome: "DTP / Tríplice Bacteriana (1º reforço)" },
      { id: "vip_ref1", nome: "VIP / Polio Inativada (1º reforço)" },
      { id: "hepa", nome: "Hepatite A (Dose única)" },
      { id: "tetraviral", nome: "Tetraviral ou SCR + Varicela (1ª dose)" }
    ]
  },
  { id: "v_48", periodo: "4 Anos", minMeses: 48, maxMeses: 999, vacinas: [
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
    details.id = "vac_details_" + p.id;
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

function interpolarLMS(arr, x) {
  // Interpolação linear apenas dentro da faixa coberta pelos dados; nunca extrapola.
  if (!Array.isArray(arr) || !arr.length || !Number.isFinite(x)) return null;
  if (x < arr[0][0] || x > arr[arr.length - 1][0]) return null;
  const i = arr.findIndex(p => p[0] >= x);
  if (i === 0) return { L: arr[0][1], M: arr[0][2], S: arr[0][3] };
  if (i < 0) return null;
  const [x0, l0, m0, s0] = arr[i - 1];
  const [x1, l1, m1, s1] = arr[i];
  if (x === x1) return { L: l1, M: m1, S: s1 };
  const f = (x - x0) / (x1 - x0);
  return { L: l0 + (l1-l0)*f, M: m0 + (m1-m0)*f, S: s0 + (s1-s0)*f };
}

function valorParaZ(z, lms) {
  if (!lms) return null;
  const {L,M,S} = lms;
  const base = 1 + L*S*z;
  if (Math.abs(L) < 1e-8) return M * Math.exp(S*z);
  if (base <= 0) return null;
  return M * Math.pow(base, 1/L);
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

function zScore(value, lms) {
  if (!(value > 0) || !lms || !(lms.M > 0) || !(lms.S > 0)) return null;
  const {L,M,S} = lms;
  const raw = Math.abs(L) < 1e-8 ? Math.log(value/M)/S : (Math.pow(value/M,L)-1)/(L*S);
  if (!Number.isFinite(raw)) return null;
  // Ajuste OMS para valores além de ±3 DP, usando a distância entre os pontos LMS ±2 e ±3.
  if (raw > 3) {
    const x2 = valorParaZ(2,lms), x3 = valorParaZ(3,lms);
    return x2 != null && x3 != null && x3 > x2 ? 3 + (value-x3)/(x3-x2) : raw;
  }
  if (raw < -3) {
    const xm3 = valorParaZ(-3,lms), xm2 = valorParaZ(-2,lms);
    return xm3 != null && xm2 != null && xm2 > xm3 ? -3 + (value-xm3)/(xm2-xm3) : raw;
  }
  return raw;
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
  if (z > 2) return { faixa: "Z > +2", desc: "Estatura elevada para a idade" };
  if (z >= -2) return { faixa: "[-2, +2]", desc: "Estatura adequada para a idade" };
  if (z >= -3) return { faixa: "[-3, -2)", desc: "Baixa estatura para a idade" };
  return { faixa: "Z < -3", desc: "Muito baixa estatura para a idade" };
}

function getInfoIMC(z, meses = null) {
  if (z == null) return { faixa: "—", desc: "—" };
  if (meses != null && meses < 60) {
    if (z > 3) return { faixa: "Z > +3", desc: "Obesidade" };
    if (z > 2) return { faixa: "+2 < Z ≤ +3", desc: "Sobrepeso" };
    if (z > 1) return { faixa: "+1 < Z ≤ +2", desc: "Risco de sobrepeso" };
    if (z >= -2) return { faixa: "−2 ≤ Z ≤ +1", desc: "Eutrofia" };
    if (z >= -3) return { faixa: "−3 ≤ Z < −2", desc: "Magreza" };
    return { faixa: "Z < −3", desc: "Magreza acentuada" };
  }
  // Faixa 5 a 19 anos (60 a 228 meses) - Metodologia OMS 2007
  if (z > 3) return { faixa: "Z > +3", desc: "Obesidade grave" };
  if (z > 2) return { faixa: "+2 < Z ≤ +3", desc: "Obesidade" };
  if (z > 1) return { faixa: "+1 < Z ≤ +2", desc: "Sobrepeso" };
  if (z >= -2) return { faixa: "−2 ≤ Z ≤ +1", desc: "Eutrofia" };
  if (z >= -3) return { faixa: "−3 ≤ Z < −2", desc: "Magreza" };
  return { faixa: "Z < −3", desc: "Magreza acentuada" };
}

function getInfoPesoComprimento(z) {
  if (z == null) return { faixa: "—", desc: "—" };
  if (z > 3) return { faixa: "Z > +3", desc: "Obesidade" };
  if (z > 2) return { faixa: "+2 < Z ≤ +3", desc: "Sobrepeso" };
  if (z > 1) return { faixa: "+1 < Z ≤ +2", desc: "Risco de sobrepeso" };
  if (z >= -2) return { faixa: "−2 ≤ Z ≤ +1", desc: "Eutrofia / Peso adequado para o comprimento" };
  if (z >= -3) return { faixa: "−3 ≤ Z < −2", desc: "Magreza" };
  return { faixa: "Z < −3", desc: "Magreza acentuada" };
}

function getInfoPC(z) {
  if (z == null) return { faixa: "—", desc: "—" };
  if (z > 2) return { faixa: "Z > +2", desc: "Macrocefalia / Acima do esperado" };
  if (z >= -2) return { faixa: "[-2, +2]", desc: "Perímetro Cefálico Adequado" };
  if (z >= -3) return { faixa: "[-3, -2)", desc: "Microcefalia / Abaixo do esperado" };
  return { faixa: "Z < -3", desc: "Microcefalia grave" };
}

$("tipo_ganho").addEventListener("change", (e) => {
  if (e.target.value === "nasc") {
    $("lbl_peso_ref").textContent = "Peso de nascimento (kg)";
  } else {
    $("lbl_peso_ref").textContent = "Peso da última consulta (kg)";
  }
});

function atualizarIdadeDisplay() {
  const el = $("idade_display");
  if (!el) return;
  const nasc = $("nasc").value;
  const data = $("data").value;
  if (!nasc || !data) {
    el.innerHTML = 'Preencha a data da consulta e data de nascimento para calcular a idade.';
    el.style.color = 'var(--text-muted)';
    return;
  }
  const age = idadeCalendario(nasc, data);
  if (!age) {
    el.innerHTML = '<span style="color:#e74c3c;">⚠️ Data da consulta anterior ao nascimento.</span>';
    return;
  }
  const ig = $("ig").value === "" ? 40 : Number($("ig").value);
  const mCrono = idadeMeses(nasc, data);
  let html = '🎂 <strong>Idade:</strong> ' + age.anos + ' ano' + (age.anos !== 1 ? 's' : '') + ', ' + age.meses + ' mês' + (age.meses !== 1 ? 'es' : '') + ' e ' + age.dias + ' dia' + (age.dias !== 1 ? 's' : '') + ' (' + Math.round(diasEntre(nasc, data)) + ' dias)';
  if (ig < 37 && mCrono <= 24) {
    const mAntropo = mCrono - ((40 - ig) * 7 / 30.4375);
    const anosCorr = Math.floor(mAntropo / 12);
    const mesesCorr = Math.floor(mAntropo % 12);
    const diasCorr = Math.round((mAntropo % 1) * 30.4375);
    html += ' &nbsp;|&nbsp; 👶 <strong>Idade corrigida (prematuro ' + ig + 's):</strong> ' + anosCorr + 'a ' + mesesCorr + 'm ' + diasCorr + 'd';
  }
  el.innerHTML = html;
  el.style.color = 'var(--text-normal)';
}

$("data").addEventListener("change", atualizarIdadeDisplay);
$("nasc").addEventListener("change", atualizarIdadeDisplay);
$("ig").addEventListener("change", atualizarIdadeDisplay);

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
  let mInfantil = mCrono;

  // Correção da prematuridade (<37 semanas) somente durante os primeiros 24 meses cronológicos.
  // DNPM e vacinação continuam usando estritamente a idade cronológica.
  const mAntropo = (ig < 37 && mCrono <= 24) ? mCrono - ((40 - ig) * 7 / 30.4375) : mCrono;

  marcosDNPM.forEach(f => {
    const el = app.querySelector("#details_" + f.id);
    if (el) el.open = (mInfantil >= f.min && mInfantil < f.max);
  });
  $("aviso_idade_dnpm").innerHTML = "Idade de avaliação do DNPM: <strong>" + fmt(mInfantil, 1) + " meses</strong>";

  calendarioVacinas.forEach(p => {
    const elVac = app.querySelector("#vac_details_" + p.id);
    if (elVac) {
      elVac.open = (mInfantil >= p.minMeses && mInfantil < p.maxMeses);
    }
  });

  const peso = $("peso").value === "" ? null : Number($("peso").value);
  const est = $("est").value === "" ? null : Number($("est").value);
  const pc = $("pc").value === "" ? null : Number($("pc").value);
  const pa = $("pa").value === "" ? null : Number($("pa").value);
  const pt = $("pt").value === "" ? null : Number($("pt").value);
  const posEst = $("pos_est").value;

  if ([peso, est, pc, pa, pt].some(v => v != null && (!Number.isFinite(v) || v <= 0))) {
    $("resultado_antropo").textContent = "Revise as medidas: valores informados devem ser números positivos.";
    return;
  }

  // Converter a medida para a posição exigida pela referência da OMS:
  // - Para < 2 anos (< 24m cronológicos), o padrão é comprimento (deitado). Se medido em pé, soma-se 0,7 cm.
  // - Para ≥ 2 anos (≥ 24m cronológicos), o padrão é estatura (em pé). Se medido deitado, subtrai-se 0,7 cm.
  let estRef = est;
  if (estRef != null) {
    if (mCrono < 24 && posEst === "em_pe") estRef += 0.7;
    else if (mCrono >= 24 && posEst === "deitado") estRef -= 0.7;
  }

  const imc = (peso != null && estRef != null && estRef > 0) ? peso / Math.pow(estRef / 100, 2) : null;

  let ganhoStr = "Não calculado.";
  const tipo = $("tipo_ganho").value;
  const pesoRef = $("peso_ref").value === "" ? null : Number($("peso_ref").value);

  if (tipo === "nasc") {
    if (pesoRef != null && peso != null) {
      const dias = diasEntre(nasc, data);
      if (dias > 0) {
        const dif = (peso - pesoRef) * 1000;
        ganhoStr = "<strong>" + fmt(dif / dias, 1) + " g/dia</strong> (" + fmt(dif, 0) + " g em " + dias + " dias desde o nascimento)";
      }
    }
  } else {
    if (dataAnt && pesoRef != null && peso != null) {
      const dias = diasEntre(dataAnt, data);
      if (dias > 0) {
        const dif = (peso - pesoRef) * 1000;
        ganhoStr = "<strong>" + fmt(dif / dias, 1) + " g/dia</strong> (" + fmt(dif, 0) + " g em " + dias + " dias desde a última consulta)";
      }
    }
  }

  const tabelasSexo = lmsOficial[sexo];

  // 1. Peso para Idade (OMS 0 a 120 meses / 0 a 10 anos)
  let zP = null;
  let infoP = { faixa: "—", desc: "—" };
  if (peso != null) {
    if (mAntropo >= 0 && mAntropo <= 120) {
      zP = zScore(peso, interpolarLMS(tabelasSexo.peso, mAntropo));
      infoP = getInfoPeso(zP);
    } else if (mAntropo > 120) {
      infoP = { faixa: "N/A", desc: "Referência OMS de peso para idade disponível até 10 anos (120m); avaliar IMC/idade" };
    } else {
      infoP = { faixa: "N/A", desc: "Idade corrigida < 0 meses (PMA < 40 semanas)" };
    }
  }

  // 2. Estatura/Comprimento para Idade (OMS 0 a 228 meses / 0 a 19 anos)
  let zE = null;
  let infoE = { faixa: "—", desc: "—" };
  if (estRef != null) {
    if (mAntropo >= 0 && mAntropo < 24) {
      zE = zScore(estRef, interpolarLMS(tabelasSexo.comp, mAntropo));
      infoE = getInfoEst(zE);
    } else if (mAntropo >= 24 && mAntropo <= 228) {
      zE = zScore(estRef, interpolarLMS(tabelasSexo.est, mAntropo));
      infoE = getInfoEst(zE);
    } else if (mAntropo > 228) {
      infoE = { faixa: "N/A", desc: "Referência OMS de estatura para idade disponível até 19 anos (228m)" };
    } else {
      infoE = { faixa: "N/A", desc: "Idade corrigida < 0 meses (PMA < 40 semanas)" };
    }
  }

  // 3. IMC para Idade (OMS 0 a 228 meses / 0 a 19 anos)
  let zI = null;
  let infoI = { faixa: "—", desc: "—" };
  if (imc != null) {
    if (mAntropo >= 0 && mAntropo < 24) {
      zI = zScore(imc, interpolarLMS(tabelasSexo.imcL, mAntropo));
      infoI = getInfoIMC(zI, mAntropo);
    } else if (mAntropo >= 24 && mAntropo <= 228) {
      zI = zScore(imc, interpolarLMS(tabelasSexo.imcH, mAntropo));
      infoI = getInfoIMC(zI, mAntropo);
    } else if (mAntropo > 228) {
      infoI = { faixa: "N/A", desc: "Referência OMS de IMC para idade disponível até 19 anos (228m)" };
    } else {
      infoI = { faixa: "N/A", desc: "Idade corrigida < 0 meses (PMA < 40 semanas)" };
    }
  }

  // 4. Perímetro Cefálico para Idade (OMS 0 a 60 meses / 0 a 5 anos)
  let zC = null;
  let infoC = { faixa: "—", desc: "—" };
  if (pc != null) {
    if (mAntropo >= 0 && mAntropo <= 60) {
      zC = zScore(pc, interpolarLMS(tabelasSexo.pc, mAntropo));
      infoC = getInfoPC(zC);
    } else if (mAntropo > 60) {
      infoC = { faixa: "N/A", desc: "Referência OMS de perímetro cefálico disponível até 5 anos (60m)" };
    } else {
      infoC = { faixa: "N/A", desc: "Idade corrigida < 0 meses (PMA < 40 semanas)" };
    }
  }

  // 5. Peso para Comprimento (OMS 45 a 110 cm, crianças < 2 anos)
  let zPC = null;
  let infoPC = { faixa: "—", desc: "—" };
  if (peso != null && estRef != null) {
    if (mCrono < 24) {
      if (estRef >= 45 && estRef <= 110) {
        zPC = zScore(peso, interpolarLMS(tabelasSexo.pesoComprimento, estRef));
        infoPC = getInfoPesoComprimento(zPC);
      } else {
        infoPC = { faixa: "N/A", desc: "Comprimento fora da faixa da tabela OMS (45 a 110 cm)" };
      }
    } else {
      infoPC = { faixa: "N/A", desc: "Para crianças ≥ 2 anos, a OMS preconiza a avaliação do IMC para idade" };
    }
  }

  cacheUltimaAntropometria = {
    peso, est, estRef, imc, pc, pa, pt,
    posEst, mCrono, mAntropo,
    zP, zE, zI, zC, zPC,
    infoP, infoE, infoI, infoC, infoPC
  };

  let infoIdade = "<strong>Paciente:</strong> " + nome + " (" + (sexo === "M" ? "Masculino" : "Feminino") + ")<br>" +
                  "<strong>Idade Cronológica:</strong> " + age.anos + "a " + age.meses + "m " + age.dias + "d (" + Math.round(diasEntre(nasc, data)) + " dias)";
  if (ig < 37 && mCrono <= 24) {
    const semCorrig = Math.round((40 - ig) * 7);
    infoIdade += "<br><strong>Idade Corrigida (Prematuro " + ig + "s):</strong> " + fmt(mAntropo, 1) + " meses (desconto de " + semCorrig + " dias aplicado até 24m)";
  }

  $("resultado_antropo").innerHTML = 
    infoIdade + "<br>" +
    "<strong>Ganho Ponderal Diário:</strong> " + ganhoStr + "<br>" +
    "<strong>Medidas Complementares:</strong> Perímetro Abdominal = " + (pa ? pa + " cm" : "—") + " | Perímetro Torácico = " + (pt ? pt + " cm" : "—") + "<br><br>" +
    "<strong>📊 Resumo Antropométrico (Padrões e Referências Oficiais da OMS):</strong><br>" +
    "<small>Tabelas incorporadas (100% offline): Peso/idade (0 a 10 anos / 0–120m); Comprimento e Estatura/idade (0 a 19 anos / 0–228m); IMC/idade (0 a 19 anos / 0–228m); Perímetro cefálico/idade (0 a 5 anos / 0–60m); Peso/comprimento (45 a 110 cm, &lt;24m). Ajuste oficial de 0,7 cm de posição (deitado vs. em pé). Correção da prematuridade (&lt;37 sem) aplicada na antropometria até 24 meses cronológicos.</small>" +
    "<table>" +
      "<thead>" +
        "<tr>" +
          "<th>Parâmetro</th>" +
          "<th>Medida</th>" +
          "<th>Z-Score Exato</th>" +
          "<th>Faixa Z</th>" +
          "<th>Classificação OMS / Caderneta</th>" +
        "</tr>" +
      "</thead>" +
      "<tbody>" +
        "<tr>" +
          "<td><strong>Peso para Idade</strong></td>" +
          "<td>" + (peso != null ? fmt(peso, 3) + " kg" : "—") + "</td>" +
          "<td>" + (peso != null ? (zP != null ? fmt(zP) : (mAntropo <= 120 ? "—" : "N/A (>10 anos)")) : "—") + "</td>" +
          "<td>" + (peso != null ? infoP.faixa : "—") + "</td>" +
          "<td>" + (peso != null ? infoP.desc : "—") + "</td>" +
        "</tr>" +
        "<tr>" +
          "<td><strong>Estatura/Comprimento</strong></td>" +
          "<td>" + (estRef != null ? fmt(estRef, 1) + " cm" + (est !== estRef ? " (" + (posEst === "em_pe" ? "+0,7cm em pé" : "−0,7cm deitado") + ")" : "") : "—") + "</td>" +
          "<td>" + (estRef != null ? (zE != null ? fmt(zE) : (mAntropo <= 228 ? "—" : "N/A (>19 anos)")) : "—") + "</td>" +
          "<td>" + (estRef != null ? infoE.faixa : "—") + "</td>" +
          "<td>" + (estRef != null ? infoE.desc : "—") + "</td>" +
        "</tr>" +
        "<tr>" +
          "<td><strong>IMC para Idade</strong></td>" +
          "<td>" + (imc != null ? fmt(imc, 2) + " kg/m²" : "—") + "</td>" +
          "<td>" + (imc != null ? (zI != null ? fmt(zI) : (mAntropo <= 228 ? "—" : "N/A (>19 anos)")) : "—") + "</td>" +
          "<td>" + (imc != null ? infoI.faixa : "—") + "</td>" +
          "<td>" + (imc != null ? infoI.desc : "—") + "</td>" +
        "</tr>" +
        "<tr>" +
          "<td><strong>Peso para Comprimento (&lt; 2 anos)</strong></td>" +
          "<td>" + (peso != null && estRef != null && mCrono < 24 ? fmt(peso, 3) + " kg / " + fmt(estRef, 1) + " cm" : "—") + "</td>" +
          "<td>" + (peso != null && estRef != null ? (mCrono < 24 ? (zPC != null ? fmt(zPC) : "Fora 45–110cm") : "N/A (≥24m)") : "—") + "</td>" +
          "<td>" + (peso != null && estRef != null ? infoPC.faixa : "—") + "</td>" +
          "<td>" + (peso != null && estRef != null ? infoPC.desc : "—") + "</td>" +
        "</tr>" +
        "<tr>" +
          "<td><strong>Perímetro Cefálico</strong></td>" +
          "<td>" + (pc != null ? fmt(pc, 1) + " cm" : "—") + "</td>" +
          "<td>" + (pc != null ? (zC != null ? fmt(zC) : (mAntropo <= 60 ? "—" : "N/A (>5 anos)")) : "—") + "</td>" +
          "<td>" + (pc != null ? infoC.faixa : "—") + "</td>" +
          "<td>" + (pc != null ? infoC.desc : "—") + "</td>" +
        "</tr>" +
      "</tbody>" +
    "</table>";

  // ── Renderizar gráficos SVG das faixas Z ──────────────────────────────
  renderizarGraficos({
    sexo, mAntropo, mCrono,
    peso, estRef, imc, pc,
    zP, zE, zI, zC, zPC,
    tabelasSexo
  });

  // ── Recomendações de conduta automáticas ─────────────────────────
  gerarRecomendacoes(mCrono, peso);
});

function renderizarGraficos({ sexo, mAntropo, mCrono, peso, estRef, imc, pc, zP, zE, zI, zC, zPC, tabelasSexo }) {
  const container = $("graficos_container");
  if (!container) return;
  container.innerHTML = "";

  // Dimensões internas do SVG (viewport lógico)
  const W = 500, H = 200, PL = 40, PR = 12, PT = 10, PB = 30;
  const gW = W - PL - PR, gH = H - PT - PB;

  // Cores das faixas
  const CORES = {
    acima3:  "#e74c3c",
    entre23: "#e67e22",
    entre12: "#f1c40f",
    normal:  "#2ecc71",
    entre_12: "#f1c40f",
    entre_23: "#e67e22",
    abaixo3: "#e74c3c"
  };

  function faixaCor(z) {
    if (z == null) return "#999";
    if (z > 3)  return CORES.acima3;
    if (z > 2)  return CORES.entre23;
    if (z > 1)  return CORES.entre12;
    if (z >= -1) return CORES.normal;
    if (z >= -2) return CORES.entre_12;
    if (z >= -3) return CORES.entre_23;
    return CORES.abaixo3;
  }

  // Gera a curva de uma tabela LMS para um intervalo de meses
  function curvaPontosLMS(tabela, xMin, xMax, zdp, steps) {
    const pts = [];
    for (let i = 0; i <= steps; i++) {
      const m = xMin + (xMax - xMin) * i / steps;
      const lms = interpolarLMS(tabela, m);
      if (!lms) continue;
      pts.push({ x: m, y: valorParaZ(zdp, lms) });
    }
    return pts;
  }

  function buildSVG(title, badge, xMin, xMax, xLabel, yMin, yMax, curvas, marcadorX, marcadorY, marcadorZ) {
    // curvas: array de { pontos:[{x,y}], cor, fill, fill2 }
    const xScale = x => PL + ((x - xMin) / (xMax - xMin)) * gW;
    const yScale = y => PT + gH - ((y - yMin) / (yMax - yMin)) * gH;

    const toPath = pts => pts.filter(p => p.y != null && Number.isFinite(p.y))
      .map((p, i) => (i === 0 ? "M" : "L") + xScale(p.x).toFixed(1) + " " + yScale(p.y).toFixed(1)).join(" ");

    let svgContent = "";

    // Faixas de fundo coloridas entre linhas Z
    curvas.forEach(c => {
      if (c.fillBetween && c.fillBetween.length === 2) {
        const [upper, lower] = c.fillBetween;
        const upPts = upper.filter(p => p.y != null && Number.isFinite(p.y));
        const loPts = lower.filter(p => p.y != null && Number.isFinite(p.y));
        if (upPts.length > 1 && loPts.length > 1) {
          const forward = upPts.map((p, i) => (i === 0 ? "M" : "L") + xScale(p.x).toFixed(1) + " " + yScale(p.y).toFixed(1)).join(" ");
          const backward = [...loPts].reverse().map((p, i) => (i === 0 ? "L" : "L") + xScale(p.x).toFixed(1) + " " + yScale(p.y).toFixed(1)).join(" ");
          svgContent += `<path d="${forward} ${backward} Z" fill="${c.cor}" opacity="0.18"/>`;
        }
      }
    });

    // Linhas Z
    curvas.forEach(c => {
      if (c.pontos && c.pontos.length > 1) {
        const d = toPath(c.pontos);
        if (d) svgContent += `<path d="${d}" fill="none" stroke="${c.cor}" stroke-width="${c.main ? 1.8 : 1}" stroke-dasharray="${c.dash || ""}"/>`;
      }
    });

    // Eixos
    svgContent += `<line x1="${PL}" y1="${PT}" x2="${PL}" y2="${PT+gH}" stroke="var(--text-muted)" stroke-width="1"/>`;
    svgContent += `<line x1="${PL}" y1="${PT+gH}" x2="${PL+gW}" y2="${PT+gH}" stroke="var(--text-muted)" stroke-width="1"/>`;

    // Ticks eixo X
    const ticksX = 6;
    for (let i = 0; i <= ticksX; i++) {
      const xv = xMin + (xMax - xMin) * i / ticksX;
      const px = xScale(xv);
      svgContent += `<line x1="${px.toFixed(1)}" y1="${PT+gH}" x2="${px.toFixed(1)}" y2="${PT+gH+4}" stroke="var(--text-muted)" stroke-width="1"/>`;
      svgContent += `<text x="${px.toFixed(1)}" y="${H-4}" text-anchor="middle" font-size="8" fill="var(--text-muted)">${Math.round(xv)}</text>`;
    }
    // Label eixo X
    svgContent += `<text x="${PL + gW/2}" y="${H}" text-anchor="middle" font-size="8" fill="var(--text-muted)">${xLabel}</text>`;

    // Ticks eixo Y (linhas Z: -3 a +3)
    [-3,-2,-1,0,1,2,3].forEach(z => {
      const yv = yMin + (yMax - yMin) * (z + 3) / 6; // linearizado
      // Usamos o valor real do ponto médio para y
    });

    // Marcador do paciente
    let marcadorSVG = "";
    if (marcadorX != null && marcadorY != null && Number.isFinite(marcadorY)) {
      const mx = xScale(marcadorX), my = yScale(marcadorY);
      const cor = faixaCor(marcadorZ);
      if (mx >= PL && mx <= PL+gW && my >= PT && my <= PT+gH) {
        // Linha vertical pontilhada
        marcadorSVG += `<line x1="${mx.toFixed(1)}" y1="${PT}" x2="${mx.toFixed(1)}" y2="${PT+gH}" stroke="${cor}" stroke-width="1" stroke-dasharray="3,3" opacity="0.7"/>`;
        // Círculo
        marcadorSVG += `<circle cx="${mx.toFixed(1)}" cy="${my.toFixed(1)}" r="5" fill="${cor}" stroke="#fff" stroke-width="1.5"/>`;
        // Label Z
        if (marcadorZ != null) {
          const zLabel = (marcadorZ > 0 ? "+" : "") + marcadorZ.toFixed(2).replace(".",",");
          const lx = (mx > PL + gW * 0.8) ? mx - 5 : mx + 5;
          const anchor = (mx > PL + gW * 0.8) ? "end" : "start";
          marcadorSVG += `<text x="${lx.toFixed(1)}" y="${(my - 7).toFixed(1)}" text-anchor="${anchor}" font-size="9" font-weight="bold" fill="${cor}">Z=${zLabel}</text>`;
        }
      }
    }

    const svg = `<svg viewBox="0 0 ${W} ${H}" xmlns="http://www.w3.org/2000/svg">${svgContent}${marcadorSVG}</svg>`;
    const corCard = marcadorZ != null ? faixaCor(marcadorZ) : "var(--background-modifier-border)";
    const card = document.createElement("div");
    card.className = "chart-card";
    card.style.borderLeft = `4px solid ${corCard}`;
    card.innerHTML = `<div class="chart-title">${title} <span class="chart-badge">${badge}</span></div>${svg}`;
    container.appendChild(card);
  }

  const STEPS = 80;

  // ── 1. Peso para Idade ────────────────────────────────────────────────
  if (peso != null && mAntropo >= 0 && mAntropo <= 120) {
    const tab = tabelasSexo.peso;
    const xMin = Math.max(0, mAntropo - 18), xMax = Math.min(120, mAntropo + 18);
    const zdps = [-3,-2,-1,0,1,2,3];
    const curvasZ = zdps.map((z, i) => ({ pontos: curvaPontosLMS(tab, xMin, xMax, z, STEPS), cor: ["#e74c3c","#e67e22","#f1c40f","#2ecc71","#f1c40f","#e67e22","#e74c3c"][i], dash: z===0?"":"4,3", main: z===0 }));
    // Faixas coloridas
    const pares = [[2,3],[1,2],[0,1],[-1,0],[-2,-1],[-3,-2]];
    const coresFaixa = [CORES.acima3, CORES.entre23, CORES.entre12, CORES.normal, CORES.entre_12, CORES.entre_23];
    pares.forEach(([lo, hi], idx) => {
      curvasZ.push({ fillBetween: [curvaPontosLMS(tab,xMin,xMax,hi,STEPS), curvaPontosLMS(tab,xMin,xMax,lo,STEPS)], cor: coresFaixa[idx] });
    });
    // Calcular yMin/yMax baseado nas curvas extremas
    const allY = curvasZ.filter(c=>c.pontos).flatMap(c=>c.pontos.map(p=>p.y)).filter(Number.isFinite);
    const yMin = Math.min(...allY) * 0.97, yMax = Math.max(...allY) * 1.03;
    const pesoLMS = interpolarLMS(tab, mAntropo);
    const pesoY = pesoLMS ? peso : null;
    buildSVG("Peso para Idade", (sexo==="M"?"♂":"♀")+" | "+fmt(peso,3)+" kg", xMin, xMax, "Meses", yMin, yMax, curvasZ, mAntropo, pesoY, zP);
  }

  // ── 2. Comprimento/Estatura para Idade ───────────────────────────────
  if (estRef != null && mAntropo >= 0 && mAntropo <= 228) {
    const useComp = mAntropo < 24;
    const tab = useComp ? tabelasSexo.comp : tabelasSexo.est;
    const tabMax = useComp ? 24 : 228;
    const xMin = Math.max(0, mAntropo - 18), xMax = Math.min(tabMax, mAntropo + 18);
    const zdps = [-3,-2,-1,0,1,2,3];
    const curvasZ = zdps.map((z, i) => ({ pontos: curvaPontosLMS(tab, xMin, xMax, z, STEPS), cor: ["#e74c3c","#e67e22","#f1c40f","#2ecc71","#f1c40f","#e67e22","#e74c3c"][i], dash: z===0?"":"4,3", main: z===0 }));
    const pares = [[2,3],[1,2],[0,1],[-1,0],[-2,-1],[-3,-2]];
    const coresFaixa = [CORES.acima3, CORES.entre23, CORES.entre12, CORES.normal, CORES.entre_12, CORES.entre_23];
    pares.forEach(([lo, hi], idx) => { curvasZ.push({ fillBetween: [curvaPontosLMS(tab,xMin,xMax,hi,STEPS), curvaPontosLMS(tab,xMin,xMax,lo,STEPS)], cor: coresFaixa[idx] }); });
    const allY = curvasZ.filter(c=>c.pontos).flatMap(c=>c.pontos.map(p=>p.y)).filter(Number.isFinite);
    const yMin = Math.min(...allY) * 0.97, yMax = Math.max(...allY) * 1.03;
    const estLMS = interpolarLMS(tab, mAntropo);
    buildSVG((useComp?"Comprimento":"Estatura")+" para Idade", (sexo==="M"?"♂":"♀")+" | "+fmt(estRef,1)+" cm", xMin, xMax, "Meses", yMin, yMax, curvasZ, mAntropo, estRef, zE);
  }

  // ── 3. IMC para Idade ─────────────────────────────────────────────────
  if (imc != null && mAntropo >= 0 && mAntropo <= 228) {
    const useComp = mAntropo < 24;
    const tab = useComp ? tabelasSexo.imcL : tabelasSexo.imcH;
    const tabMax = useComp ? 24 : 228;
    const xMin = Math.max(0, mAntropo - 18), xMax = Math.min(tabMax, mAntropo + 18);
    const zdps = [-3,-2,-1,0,1,2,3];
    const curvasZ = zdps.map((z, i) => ({ pontos: curvaPontosLMS(tab, xMin, xMax, z, STEPS), cor: ["#e74c3c","#e67e22","#f1c40f","#2ecc71","#f1c40f","#e67e22","#e74c3c"][i], dash: z===0?"":"4,3", main: z===0 }));
    const pares = [[2,3],[1,2],[0,1],[-1,0],[-2,-1],[-3,-2]];
    const coresFaixa = [CORES.acima3, CORES.entre23, CORES.entre12, CORES.normal, CORES.entre_12, CORES.entre_23];
    pares.forEach(([lo, hi], idx) => { curvasZ.push({ fillBetween: [curvaPontosLMS(tab,xMin,xMax,hi,STEPS), curvaPontosLMS(tab,xMin,xMax,lo,STEPS)], cor: coresFaixa[idx] }); });
    const allY = curvasZ.filter(c=>c.pontos).flatMap(c=>c.pontos.map(p=>p.y)).filter(Number.isFinite);
    if (allY.length > 0) {
      const yMin = Math.min(...allY) * 0.97, yMax = Math.max(...allY) * 1.03;
      buildSVG("IMC para Idade", (sexo==="M"?"♂":"♀")+" | "+fmt(imc,2)+" kg/m²", xMin, xMax, "Meses", yMin, yMax, curvasZ, mAntropo, imc, zI);
    }
  }

  // ── 4. Perímetro Cefálico para Idade ─────────────────────────────────
  if (pc != null && mAntropo >= 0 && mAntropo <= 60) {
    const tab = tabelasSexo.pc;
    const xMin = Math.max(0, mAntropo - 12), xMax = Math.min(60, mAntropo + 12);
    const zdps = [-3,-2,-1,0,1,2,3];
    const curvasZ = zdps.map((z, i) => ({ pontos: curvaPontosLMS(tab, xMin, xMax, z, STEPS), cor: ["#e74c3c","#e67e22","#f1c40f","#2ecc71","#f1c40f","#e67e22","#e74c3c"][i], dash: z===0?"":"4,3", main: z===0 }));
    const pares = [[2,3],[1,2],[0,1],[-1,0],[-2,-1],[-3,-2]];
    const coresFaixa = [CORES.acima3, CORES.entre23, CORES.entre12, CORES.normal, CORES.entre_12, CORES.entre_23];
    pares.forEach(([lo, hi], idx) => { curvasZ.push({ fillBetween: [curvaPontosLMS(tab,xMin,xMax,hi,STEPS), curvaPontosLMS(tab,xMin,xMax,lo,STEPS)], cor: coresFaixa[idx] }); });
    const allY = curvasZ.filter(c=>c.pontos).flatMap(c=>c.pontos.map(p=>p.y)).filter(Number.isFinite);
    const yMin = Math.min(...allY) * 0.97, yMax = Math.max(...allY) * 1.03;
    buildSVG("Perímetro Cefálico para Idade", (sexo==="M"?"♂":"♀")+" | "+fmt(pc,1)+" cm", xMin, xMax, "Meses", yMin, yMax, curvasZ, mAntropo, pc, zC);
  }

  // ── 5. Peso para Comprimento ─────────────────────────────────────────
  if (peso != null && estRef != null && mCrono < 24 && zPC != null) {
    const tab = tabelasSexo.pesoComprimento;
    const xMin = Math.max(45, estRef - 15), xMax = Math.min(110, estRef + 15);
    const zdps = [-3,-2,-1,0,1,2,3];
    const curvasZ = zdps.map((z, i) => ({ pontos: curvaPontosLMS(tab, xMin, xMax, z, STEPS), cor: ["#e74c3c","#e67e22","#f1c40f","#2ecc71","#f1c40f","#e67e22","#e74c3c"][i], dash: z===0?"":"4,3", main: z===0 }));
    const pares = [[2,3],[1,2],[0,1],[-1,0],[-2,-1],[-3,-2]];
    const coresFaixa = [CORES.acima3, CORES.entre23, CORES.entre12, CORES.normal, CORES.entre_12, CORES.entre_23];
    pares.forEach(([lo, hi], idx) => { curvasZ.push({ fillBetween: [curvaPontosLMS(tab,xMin,xMax,hi,STEPS), curvaPontosLMS(tab,xMin,xMax,lo,STEPS)], cor: coresFaixa[idx] }); });
    const allY = curvasZ.filter(c=>c.pontos).flatMap(c=>c.pontos.map(p=>p.y)).filter(Number.isFinite);
    if (allY.length > 0) {
      const yMin = Math.min(...allY) * 0.97, yMax = Math.max(...allY) * 1.03;
      buildSVG("Peso para Comprimento", (sexo==="M"?"♂":"♀")+" | "+fmt(peso,3)+" kg / "+fmt(estRef,1)+" cm", xMin, xMax, "Comprimento (cm)", yMin, yMax, curvasZ, estRef, peso, zPC);
    }
  }
}

function gerarRecomendacoes(mCrono, peso) {
  const el = $("recomendacoes_container");
  if (!el) return;

  const recomendacoes = [];

  // ── Suplementação Profilática (SBP / MS) ──────────────────────
  const suplementos = [];

  // Vitamina D
  if (mCrono < 12) {
    suplementos.push({ icone: "🌞", nome: "Vitamina D", dose: "400 UI/dia", obs: "Iniciar nos primeiros dias de vida, manter até 1 ano." });
  } else if (mCrono < 216) { // até 18 anos (216 meses)
    suplementos.push({ icone: "🌞", nome: "Vitamina D", dose: "600 UI/dia", obs: "1 a 18 anos. Avaliar exposição solar e dosagem sérica se necessário." });
  }

  // Ferro elementar (6m a 24m)
  if (mCrono >= 6 && mCrono < 24) {
    const doseFe = peso != null && peso > 0
      ? "1 mg/kg/dia = " + fmt(peso * 1, 1) + " mg/dia"
      : "1 mg/kg/dia (preencha o peso para calcular a dose exata)";
    suplementos.push({ icone: "🔴", nome: "Ferro Elementar", dose: doseFe, obs: "6 meses a 2 anos. Preferêncialmente em jejum, afastado 1h de leite. Pode causar coloração escura das fezes." });
  }

  if (suplementos.length > 0) {
    recomendacoes.push({ titulo: "📊 Suplementação Profilática (SBP / MS)", itens: suplementos });
  }

  // ── Renderização das recomendações ─────────────────────────────
  if (recomendacoes.length === 0) {
    el.innerHTML = "";
    return;
  }

  let html = '<hr style="margin: 20px 0; border: 0; border-top: 1px dashed var(--background-modifier-border);">';
  html += '<h4 style="margin: 16px 0 10px; color: var(--text-normal);">📋 Recomendações de Conduta Automatizadas</h4>';
  html += '<p style="font-size:0.82em; color:var(--text-muted); margin-bottom:12px;">Geradas automaticamente com base na idade cronológica calculada. Revise sempre com o contexto clínico individual.</p>';

  recomendacoes.forEach(grupo => {
    html += '<fieldset style="margin-bottom:12px; border:1px solid var(--background-modifier-border); border-radius:6px; padding:12px;">';
    html += '<legend style="font-size:.85em; font-weight:bold; padding:0 6px;">' + grupo.titulo + '</legend>';
    html += '<table style="width:100%; border-collapse:collapse; font-size:0.88em;">';
    html += '<thead><tr>';
    html += '<th style="border:1px solid var(--background-modifier-border); padding:6px 8px; background:var(--background-secondary-alt); width:30%;">Nutriente</th>';
    html += '<th style="border:1px solid var(--background-modifier-border); padding:6px 8px; background:var(--background-secondary-alt); width:25%;">Dose Recomendada</th>';
    html += '<th style="border:1px solid var(--background-modifier-border); padding:6px 8px; background:var(--background-secondary-alt);">Observações</th>';
    html += '</tr></thead><tbody>';
    grupo.itens.forEach(item => {
      html += '<tr>';
      html += '<td style="border:1px solid var(--background-modifier-border); padding:6px 8px; font-weight:bold;">' + item.icone + ' ' + item.nome + '</td>';
      html += '<td style="border:1px solid var(--background-modifier-border); padding:6px 8px; color:var(--interactive-accent); font-weight:bold;">' + item.dose + '</td>';
      html += '<td style="border:1px solid var(--background-modifier-border); padding:6px 8px; color:var(--text-muted); font-size:0.9em;">' + item.obs + '</td>';
      html += '</tr>';
    });
    html += '</tbody></table></fieldset>';
  });

  el.innerHTML = html;
}

$("calcular_dnpm").addEventListener("click", () => {
  const nasc = $("nasc").value;
  const data = $("data").value;
  if (!nasc || !data) {
    $("resultado_dnpm").textContent = "Por favor, preencha a data de nascimento no topo para realizar a avaliação do DNPM.";
    return;
  }
  let mInfantil = idadeMeses(nasc, data);
  const faixaAtual = marcosDNPM.find(f => mInfantil >= f.min && mInfantil < f.max);
  if (!faixaAtual) {
    $("resultado_dnpm").innerHTML = "Idade de avaliação: <strong>" + fmt(mInfantil,1) + " meses</strong>. Fora da faixa de marcos rastreados da Caderneta (0 a 36 meses).";
    return;
  }

  const checkboxes = app.querySelectorAll('input[data-faixa="' + faixaAtual.id + '"]');
  let totalMarcos = 0, marcadosNormais = 0, alertasMarcados = 0;
  checkboxes.forEach(chk => {
    const isAlerta = chk.getAttribute("data-alerta") === "true";
    if (isAlerta) { if (chk.checked) alertasMarcados++; }
    else { totalMarcos++; if (chk.checked) marcadosNormais++; }
  });

  let statusHtml = "";
  if (alertasMarcados > 0) {
    statusHtml = '<span style="color:#e74c3c; font-weight:bold;">🚨 DESENVOLVIMENTO COM SINAL DE ALERTA / RISCO</span><br>Foi identificado pelo menos 1 sinal de risco/alerta importante para a faixa etária.';
  } else if (marcadosNormais === totalMarcos) {
    statusHtml = '<span style="color:#27ae60; font-weight:bold;">✅ DESENVOLVIMENTO ADEQUADO PARA A FAIXA ETÁRIA</span><br>A criança cumpre todos os marcos esperados para ' + faixaAtual.label + '.';
  } else {
    statusHtml = '<span style="color:#e74c3c; font-weight:bold;">🚨 PROVÁVEL ATRASO NO DESENVOLVIMENTO</span><br>Ausência da maioria dos marcos previstos para ' + faixaAtual.label + ' (' + marcadosNormais + '/' + totalMarcos + ').';
  }

  $("resultado_dnpm").innerHTML = "<strong>Avaliação do DNPM (" + faixaAtual.label + "):</strong><br>Idade de Referência: <strong>" + fmt(mInfantil, 1) + " meses</strong><br><br>" + statusHtml;
});

$("validar_vacinas").addEventListener("click", () => {
  const nasc = $("nasc").value;
  const data = $("data").value;
  if (!nasc || !data) {
    $("resultado_vacinas").textContent = "Preencha a data de nascimento no topo para validar a carteira vacinal.";
    return;
  }
  let mCrono = idadeMeses(nasc, data);
  let vacinasEmAtraso = [], vacinasDevidasCount = 0;
  calendarioVacinas.forEach(p => {
    if (mCrono >= p.minMeses) {
      p.vacinas.forEach(v => {
        vacinasDevidasCount++;
        const chk = $("vac_" + v.id);
        if (!chk || !chk.checked) {
          vacinasEmAtraso.push(v.nome + " (" + p.periodo + ")");
        }
      });
    }
  });

  let htmlRes = vacinasEmAtraso.length === 0 ? 
    '<span style="color:#27ae60; font-weight:bold;">✅ HISTÓRICO VACINAL ADEQUADO / EM DIA</span><br>Todas as ' + vacinasDevidasCount + ' vacinas previstas estão em dia.' :
    '<span style="color:#e74c3c; font-weight:bold;">⚠️ VACINAS EM ATRASO</span><br>Pendente(s):<ul style="margin-top:6px; margin-bottom:0; padding-left:20px;">' + vacinasEmAtraso.map(v => '<li>' + v + '</li>').join("") + '</ul>';

  $("resultado_vacinas").innerHTML = htmlRes;
});


$("gerar_relatorio").addEventListener("click", () => {
  const nome = $("nome_paciente").value || "Paciente Pediátrico";
  const sexo = $("sexo").value === "M" ? "Masculino" : "Feminino";
  const nasc = $("nasc").value || "N/A";
  const data = $("data").value || "N/A";
  const ig = $("ig").value === "" ? 40 : Number($("ig").value);

  const hma = $("hma").value || "Não relatada";
  const hpp = $("hpp").value || "Não relatada";
  const habAlimentacao = $("hab_alimentacao").value || "Não informado";
  const habFormula = $("hab_formula").value || "Não informado";
  const habSono = $("hab_sono").value || "Não informado";
  const habFraldas = $("hab_fraldas").value || "Não informado";

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
  const acSel = $("ac_select").value;
  const acStr = acSel === "OUTRO" ? ($("ac_desc").value || "Sem alterações") : acSel;

  const fr = $("fr").value;
  const apSel = $("ap_select").value;
  const apStr = apSel === "OUTRO" ? ($("ap_desc").value || "Sem alterações") : apSel;

  const otoSel = $("oto_select").value;
  const otoStr = otoSel === "OUTRO" ? ($("oto_outro").value || "Sem alterações") : otoSel;

  const rinoSel = $("rino_select").value;
  const rinoStr = rinoSel === "OUTRO" ? ($("rino_outro").value || "Sem alterações") : rinoSel;

  const oroSel = $("oro_select").value;
  const oroStr = oroSel === "OUTRO" ? ($("oro_outro").value || "Sem alterações") : oroSel;

  const genLivre = $("gen_desc_livre").value || "Sem alterações aparentes";

  let tannerStr = sexo === "Feminino" ? "Mamas: " + $("tanner_m").value + " | Pelos: " + $("tanner_pf").value : "Genitália: " + $("tanner_g").value + " | Pelos: " + $("tanner_pm").value;

  let text = "AVALIAÇÃO DE PUERICULTURA E EXAME FÍSICO PEDIÁTRICO\n";
  text += "===================================================\n";
  text += "IDENTIFICAÇÃO:\n";
  text += "- Nome: " + nome + "\n";
  text += "- Sexo: " + sexo + " | Nascimento: " + nasc + " | Data Consulta: " + data + "\n";
  text += "- Idade Gestacional ao Nascer: " + ig + " semanas" + (ig < 37 ? " (Prematuro)" : " (A termo)") + "\n\n";

  text += "ANAMNESE:\n- HMA:\n" + hma + "\n\n- HPP:\n" + hpp + "\n\n";
  text += "HÁBITOS E ESTILO DE VIDA:\n";
  text += "- Alimentação: " + habAlimentacao + " | Fórmula: " + habFormula + "\n";
  text += "- Sono: " + habSono + " | Fraldas: " + habFraldas + "\n\n";

  text += "AVALIAÇÃO DO DESENVOLVIMENTO (DNPM):\n" + $("resultado_dnpm").innerText + "\n\n";
  text += "HISTÓRICO VACINAL:\n" + $("resultado_vacinas").innerText + "\n\n";

  text += "ANTROPOMETRIA (Referências Oficiais da OMS):\n";
  text += "- Peso: " + (peso ? peso + " kg" : "N/I") + " | Estatura: " + (est ? est + " cm" : "N/I") + "\n";
  text += "- Perímetro Cefálico: " + (pc ? pc + " cm" : "N/I") + "\n";
  text += "- Posição da medida comprimento/estatura: " + $("pos_est").selectedOptions[0].text + "\n";
  text += "- Fontanela Anterior: " + faStatus + (faVal ? " (" + faVal + " " + faUnid + ")" : "") + "\n";
  text += "- Fontanela Posterior: " + fpStatus + (fpVal ? " (" + fpVal + " " + fpUnid + ")" : "") + "\n";

  if (cacheUltimaAntropometria) {
    const c = cacheUltimaAntropometria;
    text += "\n  [Z-Scores Antropométricos Calculados (OMS / SISVAN)]:\n";
    text += "  * Peso/Idade: " + (c.zP != null ? "Z = " + fmt(c.zP) + " | Faixa: " + c.infoP.faixa + " (" + c.infoP.desc + ")" : c.infoP.desc) + "\n";
    text += "  * Estatura/Idade: " + (c.zE != null ? "Z = " + fmt(c.zE) + " | Faixa: " + c.infoE.faixa + " (" + c.infoE.desc + ")" : c.infoE.desc) + "\n";
    text += "  * IMC/Idade: " + (c.zI != null ? "Z = " + fmt(c.zI) + " | Faixa: " + c.infoI.faixa + " (" + c.infoI.desc + ")" : c.infoI.desc) + "\n";
    text += "  * Peso/Comprimento: " + (c.zPC != null ? "Z = " + fmt(c.zPC) + " | Faixa: " + c.infoPC.faixa + " (" + c.infoPC.desc + ")" : c.infoPC.desc) + "\n";
    text += "  * PC/Idade: " + (c.zC != null ? "Z = " + fmt(c.zC) + " | Faixa: " + c.infoC.faixa + " (" + c.infoC.desc + ")" : c.infoC.desc) + "\n";
  }
  text += "\n";

  // Recomendações de conduta
  const recEl = $("recomendacoes_container");
  if (recEl && recEl.innerText && recEl.innerText.trim()) {
    text += "RECOMENDAÇÕES DE CONDUTA (automáticas):\n";
    text += recEl.innerText.trim() + "\n\n";
  }

  text += "EXAME FÍSICO:\n";
  text += "1. Cardiovascular: FC = " + (fc ? fc + " bpm" : "N/I") + " | Ausculta: " + acStr + "\n";
  text += "2. Respiratório: FR = " + (fr ? fr + " ipm" : "N/I") + " | Ausculta: " + apStr + "\n";
  text += "3. ORL: Otoscopia: " + otoStr + " | Rinoscopia: " + rinoStr + " | Oroscopia: " + oroStr + "\n";
  text += "4. Genitália & Tanner: " + tannerStr + " | Descrição: " + genLivre + "\n";
  text += "===================================================";

  $("box_relatorio").innerText = text;
});

$("copiar_relatorio").addEventListener("click", () => {
  const relatorioText = $("box_relatorio").innerText;
  if (!relatorioText || relatorioText.includes("Clique no botão acima")) {
    alert("Clique em 'Gerar Relatório Clínico Completo' antes de copiar.");
    return;
  }
  navigator.clipboard.writeText(relatorioText).then(() => {
    alert("Relatório copiado com sucesso para a Área de Transferência!");
  });
});
```
