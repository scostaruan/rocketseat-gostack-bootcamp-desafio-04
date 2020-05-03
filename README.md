# Desafio 04 - Conceitos do React Native

Nesse desafio, você deve criar uma aplicação para treinar o que você aprendeu até agora no React Native!

Agora você deve continuar desenvolvendo a aplicação que irá armazenar repositórios do seu portfólio, que você já desenvolveu o backend utilizando o Node.js, e no último desafio em ReactJS.

## Funcionalidades da aplicação

Código para atingir os objetivos de cada funcionalidade.

### `Listar os repositórios da sua API`

Deve ser capaz de criar uma lista de todos os repositórios que estão cadastrados na sua API com os campos **title**, **techs** e número de **likes** seguindo o padrão `${repository.likes}` curtidas, apenas alterando o número para ser dinâmico.

```javascript
useEffect(() => {
  api.get("repositories").then((response) => {
    setRepositories(response.data);
  });
}, []);
```

### `Curtir um repositório listado da API`

Deve ser capaz de curtir um item na sua API através de um botão com o texto _Curtir_ e deve atualizar o número de **likes** na listagem no mobile.

```javascript
async function handleLikeRepository(id) {
  const response = await api.post(`/repositories/${id}/like`);

  console.log(response.data.likes);

  repositoriesData = [...repositories];

  const repositoryDataIndex = repositoriesData.findIndex(
    (repositoryData) => repositoryData.id === id
  );

  if (repositoryDataIndex < 0) {
    return response.status(400).json({ error: "Repository not found." });
  }

  repositoriesData[repositoryDataIndex].likes = response.data.likes;

  setRepositories(repositoriesData);
}
```

---

**Created by** `costaruan`
