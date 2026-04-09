# 🔗 Documentação de Integração : Hubmanager

---

## 📄 Descrição

Este documento descreve os endpoints necessários para que o sistema Hubmanager realize a sincronização de residentes, visitantes e faces para o ecossistema Condlink.

---

## 🔐 Autenticação

Todas as requisições devem conter o header:

```
X-GUARDIAN-KEY: 12DE-76XD-98HJ-00P0

Content-Type: application/json (ou multipart/form-data para upload de arquivos)
```

---

## 👥 Cadastro de Residentes

Cadastro de Residentes (Condôminos)
Para criar ou integrar um residente do Hubmanager no Condlink.

Endpoint: POST /v1/condominio/item/create

Base URL: https://us-central1-earnest-cosmos-175020.cloudfunctions.net/sindico-gerente-controle-acesso-condominio

Payload (Form-Data):
| Campo | Tipo | Descrição |
| :---: | :---: | :---: |
| File | File | Arquivo de imagem/foto do residente |
| idCondominio | String | ID do condomínio no sistema Condlink |
| nome | String | Nome completo do residente |
| tipoResponsavel |String | Ex: "Administrador", "Morador" |

---

## 📥 Sincronização de Visitantes e Biofaces

Para enviar a face de um visitante ou residente diretamente para um hardware específico (Gateway/FaceID).

Endpoint: POST /hikvision-crud/insertUser

Base URL: https://us-central1-earnest-cosmos-175020.cloudfunctions.net

Exemplo de JSON:

```http
{
  "data": {
    "devID": "ID_DO_HARDWARE",
    "idUser": "ID_NO_HUBMANAGER",
    "name": "Nome do Visitante",
    "photo": "https://url-da-imagem.com.br/foto.jpg"
  }
}
```

### 📑 Consulta de Hardwares Disponíveis

Utilizado para listar os dispositivos ativos onde o acesso pode ser liberado.
```http
Endpoint: GET /v1/hardware/list

Parâmetro: idCondominio={ID}
```
Exemplo de Resposta:

```http
{
  "hardwares": [
    {
      "alias": "Entrada Principal",
      "devID": "883382",
      "modelo": "iDAccess Pro",
      "status": "ativo",
      "online": "conectado"
    }
  ]
}

```