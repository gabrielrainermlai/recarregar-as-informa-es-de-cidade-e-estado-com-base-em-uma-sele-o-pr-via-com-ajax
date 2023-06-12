# recarregar-as-informa-es-de-cidade-e-estado-com-base-em-uma-sele-o-pr-via-com-ajax
Aqui está um exemplo de como usar o Ajax com XMLHttpRequest para recarregar as informações de cidade e estado com base em uma seleção prévia:


Para obter as informações de cidade e estado com base no IBGE, você pode utilizar a API do IBGE, que fornece acesso aos dados de localidades brasileiras.

Aqui está um exemplo de como adaptar o código anterior para carregar as informações de cidade e estado usando a API do IBGE:

HTML:
```html
<!DOCTYPE html>
<html>
<head>
  <title>Exemplo de Recarga Cidade e Estado</title>
  <script>
    function carregarCidades() {
      var estado = document.getElementById("estado").value;
      var xmlhttp = new XMLHttpRequest();
      
      xmlhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
          var cidades = JSON.parse(this.responseText);
          var options = "";
          
          for (var i = 0; i < cidades.length; i++) {
            options += "<option value='" + cidades[i].id + "'>" + cidades[i].nome + "</option>";
          }
          
          document.getElementById("cidade").innerHTML = options;
        }
      };
      
      xmlhttp.open("GET", "https://servicodados.ibge.gov.br/api/v1/localidades/estados/" + estado + "/municipios", true);
      xmlhttp.send();
    }
  </script>
</head>
<body>
  <label for="estado">Estado:</label>
  <select id="estado" onchange="carregarCidades()">
    <option value="SP">São Paulo</option>
    <option value="RJ">Rio de Janeiro</option>
    <option value="MG">Minas Gerais</option>
  </select>
  
  <br>
  
  <label for="cidade">Cidade:</label>
  <select id="cidade"></select>
</body>
</html>
```

Neste exemplo, usamos a API do IBGE para obter as cidades com base no estado selecionado. Fazemos uma requisição GET para a URL "https://servicodados.ibge.gov.br/api/v1/localidades/estados/" + estado + "/municipios", onde "estado" é o valor selecionado no campo select.

A resposta da API é recebida pelo JavaScript e, quando a solicitação é concluída com sucesso (estado `readyState` igual a 4 e status igual a 200), o conteúdo retornado é transformado em um objeto JavaScript usando `JSON.parse()`. Em seguida, iteramos sobre o array de cidades e construímos as opções para o select de cidade.

As opções de cidade são adicionadas ao select de cidade através da manipulação do `innerHTML`.

Dessa forma, ao selecionar um estado, as cidades correspondentes serão carregadas dinamicamente usando a API do IBGE. Certifique-se de que o código esteja sendo executado em um servidor ou hospedado em um domínio permitido pela política de segurança do navegador para fazer requisições para a API do IBGE.
