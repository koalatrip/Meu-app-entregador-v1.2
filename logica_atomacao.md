# 📑 LÓGICA DE CONFIGURAÇÃO - AUTOMAÇÃO LALAMOVE (v2.0)

Este documento contém as métricas de decisão para o Assistente de Tela (Círculo Flutuante). 
Edite os valores abaixo sempre que houver mudança nos custos operacionais.

---

## 🛠️ PARÂMETROS EDITÁVEIS (MÉTRICAS)
- *COMISSAO_APP:* 0.20  (Taxa padrão de 20% da Lalamove)
- *PRECO_GASOLINA:* 6.80 (Valor atualizado por litro em R$)
- *CONSUMO_VEICULO:* 10.0 (KM por litro médio do seu veículo)
- *CUSTO_POR_KM_GAS:* 0.68 (Calculado: 6.80 / 10)

---

## 📉 FÓRMULA DE CÁLCULO INSTANTÂNEO
A automação no Android deve processar os dados da tela seguindo esta lógica:

1. *CAPTURAR:* Valor_Oferta e Distancia_KM (via AutoInput).
2. *DESCONTAR_TAXA:* GANHO_LIMPO = Valor_Oferta * 0.80.
3. *CALCULAR_GASOLINA:* GASTO_GAS = Distancia_KM * 0.68.
4. *LUCRO_FINAL:* SOBRA_REAL = GANHO_LIMPO - GASTO_GAS.
5. *EFICIÊNCIA:* RESULTADO_POR_KM = SOBRA_REAL / Distancia_KM.

---

## 🚦 CRITÉRIOS DO CÍRCULO (OVERLAY)
Configuração de cores para o botão flutuante:

- *🟢 VERDE (Boa):* RESULTADO_POR_KM >= 1.80  
  Foco total aqui para atingir a meta de R$ 10.000.

- *🟡 AMARELO (Média):* RESULTADO_POR_KM >= 1.30 E < 1.80  
  Avaliar se o destino é favorável para novas corridas.

- *🔴 VERMELHO (Ruim):* RESULTADO_POR_KM < 1.30  
  Alerta: Baixa lucratividade considerando o novo preço da gasolina.

---

## 📲 PRÓXIMOS PASSOS NO ANDROID
1. *No Tasker:* Criar uma "Cena" (Scene) com um elemento circular.
2. *No AutoInput:* Configurar a "Query UI" para ler o app da Lalamove.
3. *Vincular:* Fazer a cor da Cena mudar com base na variável %RESULTADO_POR_KM.
