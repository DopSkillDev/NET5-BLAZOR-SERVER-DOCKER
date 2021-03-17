# Introdução ao ASP.NET Core Blazor Server com Docker

* Bem-vindo ao Blazor! *

![](https://user-images.githubusercontent.com/52793184/111456254-86b43a80-86f5-11eb-9745-9558d0ea0caa.png)

Blazor é uma estrutura para a construção de IU da web interativa do lado do cliente com [.NET] (/ dotnet / standard / tour):

* Crie interfaces de usuário interativas avançadas usando [C #] (/ dotnet / csharp /) em vez de [JavaScript] (https://www.javascript.com).
* Compartilhe a lógica do aplicativo do lado do servidor e do lado do cliente escrita em .NET.
* Renderize a IU como HTML e CSS para amplo suporte a navegadores, incluindo navegadores móveis.
* Integre com plataformas de hospedagem modernas, como [Docker] (/ dotnet / standard / microservices-architecture / container-docker-Introduction / index).

O uso do .NET para desenvolvimento da Web do lado do cliente oferece as seguintes vantagens:

* Escreva código em C # em vez de JavaScript.
* Aproveite o ecossistema .NET existente de [bibliotecas .NET] (/ dotnet / standard / class-libraries).
* Compartilhe a lógica do aplicativo no servidor e no cliente.
* Beneficie-se do desempenho, confiabilidade e segurança do .NET.
* Mantenha a produtividade com o [Visual Studio] (https://visualstudio.microsoft.com) no Windows, Linux e macOS.
* Construa em um conjunto comum de linguagens, estruturas e ferramentas que são estáveis, ricas em recursos e fáceis de usar.

## Componentes

Os aplicativos Blazor são baseados em * componentes *. Um componente no Blazor é um elemento da IU, como uma página, caixa de diálogo ou formulário de entrada de dados.

Os componentes são classes .NET C # construídas em [.NET assemblies] (/ dotnet / standard / assembly /) que:

* Defina uma lógica de renderização de IU flexível.
* Lidar com eventos do usuário.
* Pode ser aninhado e reutilizado.
* Pode ser compartilhado e distribuído como [bibliotecas de classes Razor] (xref: razor-pages / ui-class) ou [pacotes NuGet] (/ nuget / what-is-nuget).

A classe do componente é geralmente escrita na forma de uma página de marcação [Razor] (xref: mvc / views / razor) com uma extensão de arquivo `.razor`. Os componentes no Blazor são formalmente chamados de * componentes do Razor *. Razor é uma sintaxe para combinar marcação HTML com código C # projetado para produtividade do desenvolvedor. O Razor permite que você alterne entre marcação HTML e C # no mesmo arquivo com suporte de programação [IntelliSense] (/ visualstudio / ide / using-intellisense) no Visual Studio. Razor Pages e MVC também usam Razor. Ao contrário do Razor Pages e MVC, que são construídos em torno de um modelo de solicitação / resposta, os componentes são usados ​​especificamente para a lógica e composição da IU do lado do cliente.

O Blazor usa tags HTML naturais para composição da IU. A seguinte marcação do Razor demonstra um componente (`Dialog.razor`) que exibe uma caixa de diálogo e processa um evento quando o usuário seleciona um botão:

`` `navalha
<div class = "card" style = "width: 22rem">
    <div class = "card-body">
        <h3 class = "card-title"> @ Título </h3>
        <p class = "card-text"> @ ChildContent </p>
        <button @ onclick = "OnYes"> Sim! </button>
    </div>
</div>

@code {
    [Parâmetro]
    public RenderFragment ChildContent {get; definir; }

    [Parâmetro]
    public string Title {get; definir; }

    privado vazio Sim ()
    {
        Console.WriteLine ("Gravar no console em C #! Botão 'Sim' selecionado.");
    }
}
`` `

No exemplo anterior, `OnYes` é um método C # disparado pelo evento` onclick` do botão. O texto da caixa de diálogo (`ChildContent`) e o título (` Title`) são fornecidos pelo seguinte componente que usa este componente em sua UI.

O componente `Dialog` é aninhado em outro componente usando uma tag HTML. No exemplo a seguir, o componente `Index` (` Pages / Index.razor`) usa o componente `Dialog` anterior. O atributo `Title` da tag passa um valor para o título para a propriedade` Title` do componente `Dialog`. O texto do componente `Dialog` (` ChildContent`) é definido pelo conteúdo do elemento `<Dialog>`. Quando o componente `Dialog` é adicionado ao componente` Index`, [IntelliSense no Visual Studio] (/ visualstudio / ide / using-intellisense) acelera o desenvolvimento com sintaxe e conclusão de parâmetro.

`` `navalha
@página "/"

<h1> Olá, mundo! </h1>

<p>
    Bem-vindo ao seu novo aplicativo.
</p>

<Dialog Title = "Saiba mais">
    Quer <i> aprender mais </i> sobre o Blazor?
</Dialog>
`` `

A caixa de diálogo é renderizada quando o componente `Index` é acessado em um navegador. Quando o botão é selecionado pelo usuário, o console de ferramentas do desenvolvedor do navegador mostra a mensagem escrita pelo método `OnYes`:

! [Componente de diálogo renderizado no navegador aninhado dentro do componente Índice. O console de ferramentas do desenvolvedor do navegador mostra a mensagem escrita pelo código C # quando o usuário seleciona Sim! botão na IU.] (index / _static / dialog.png)

Os componentes são renderizados em uma representação na memória do [Document Object Model (DOM)] do navegador (https://developer.mozilla.org/docs/Web/API/Document_Object_Model/Introduction) chamada de * árvore de renderização *, que i