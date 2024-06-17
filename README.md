Para exemplificar como criar uma classe `Pessoa` em C# e escrever testes unitários para ela utilizando xUnit, vamos seguir os passos abaixo. A classe `Pessoa` será simples, com algumas propriedades básicas e métodos típicos que poderíamos querer testar.

### Passos

1. **Configurar o Ambiente:**
   - Certifique-se de ter o Visual Studio instalado.
   - Crie um novo projeto de biblioteca de classes para a classe `Pessoa`.
   - Crie um novo projeto de testes unitários no mesmo solution.

2. **Instalar o xUnit:**
   - No Visual Studio, abra o **NuGet Package Manager** para o projeto de testes.
   - Instale os pacotes `xunit` e `xunit.runner.visualstudio`.

3. **Escrever a Classe `Pessoa`:**

```csharp
// Arquivo: Pessoa.cs
public class Pessoa
{
    public string Nome { get; set; }
    public int Idade { get; private set; }

    public Pessoa(string nome, int idade)
    {
        Nome = nome;
        Idade = idade;
    }

    public void FazerAniversario()
    {
        Idade++;
    }

    public bool EhMaiorDeIdade()
    {
        return Idade >= 18;
    }
}
```

4. **Escrever os Testes Unitários com xUnit:**

Vamos criar testes para verificar se a classe `Pessoa` funciona conforme esperado. Criaremos um arquivo `PessoaTests.cs` no projeto de testes para isso.

```csharp
// Arquivo: PessoaTests.cs
using Xunit;

namespace SeuProjeto.Testes
{
    public class PessoaTests
    {
        [Fact]
        public void Construtor_DeveInicializarPropriedadesCorretamente()
        {
            // Arrange
            string nome = "João";
            int idade = 30;

            // Act
            var pessoa = new Pessoa(nome, idade);

            // Assert
            Assert.Equal(nome, pessoa.Nome);
            Assert.Equal(idade, pessoa.Idade);
        }

        [Fact]
        public void FazerAniversario_DeveIncrementarIdade()
        {
            // Arrange
            var pessoa = new Pessoa("Maria", 25);
            int idadeInicial = pessoa.Idade;

            // Act
            pessoa.FazerAniversario();

            // Assert
            Assert.Equal(idadeInicial + 1, pessoa.Idade);
        }

        [Theory]
        [InlineData(20, true)]
        [InlineData(17, false)]
        [InlineData(18, true)]
        [InlineData(19, true)]
        public void EhMaiorDeIdade_DeveRetornarCorretamente(int idade, bool esperado)
        {
            // Arrange
            var pessoa = new Pessoa("José", idade);

            // Act
            bool resultado = pessoa.EhMaiorDeIdade();

            // Assert
            Assert.Equal(esperado, resultado);
        }
    }
}
```

### Estrutura dos Testes com xUnit:

- **[Fact]**: Atributo que indica um método de teste simples. Cada método marcado com `[Fact]` é um teste unitário.
- **[Theory]** e **[InlineData]**: xUnit permite usar teorias e data-driven tests para testar o mesmo método com diferentes inputs.

### Rodando os Testes:

1. **Abrir a Janela de Teste:**
   - No Visual Studio, vá para **Test > Test Explorer**.

2. **Executar os Testes:**
   - No **Test Explorer**, clique em **Run All** para executar todos os testes.
   - Os resultados dos testes aparecerão na janela do **Test Explorer**, indicando quais testes passaram e quais falharam.

### Resumo

- **Configuração:** Criar projetos de biblioteca de classes e de testes.
- **Instalação:** Adicionar xUnit via NuGet.
- **Código:** Escrever a classe `Pessoa` com suas propriedades e métodos.
- **Testes:** Escrever métodos de teste utilizando `[Fact]` e `[Theory]` para verificar cada funcionalidade da classe.
- **Execução:** Rodar os testes e verificar os resultados.

Com esses passos, você pode começar a criar e executar testes unitários eficazes para suas classes em C# usando o framework xUnit. Este método é essencial para garantir a funcionalidade correta do código e facilita a manutenção e evolução do seu projeto.
