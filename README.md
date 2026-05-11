# apresentacao-bim2-2026a-laulugoch

## Parte prática

### Ambiente utilizado
Para executar os códigos da aula, eu utilizei o VS Code com extensão para Java. Escolhi este ambiente por já estar familiarizada com ele em outras disciplinas.

Comandos:
- Compilar: `javac GenerateStudentData.java`
- Executar: `java GenerateStudentData`

### Execução
**StudentGrades.java**  
O programa lê o arquivo `students.csv`, cria objetos da classe `Student` para cada estudante e depois calcula a média das notas.

![código 1](StudentGrades.gif)

**GenerateStudentData.java**  
O programa acessa uma API na internet para gerar nomes aleatórios de pessoas brasileiras. Depois disso, ele cria objetos da classe `Student`, gera notas aleatórias entre 5 e 10 e salva tudo em um arquivo CSV.

![código 2](GenerateStudentData.gif)

## Parte teórica
### Perguntas do segundo código
**5. O que faz o código random.nextDouble()?**

Primeiramente, é criado o objeto `Random random = new Random();`, que possui como um de seus métodos o `nextDouble()`.
O método `nextDouble()` retorna um número decimal aleatório entre: 0.0 (inclusive) e 1.0 (exclusive)

No programa, ele aparece nesta linha: `double grade = 5 + random.nextDouble() * 5;`

Nesse caso, o valor gerado por `nextDouble()` é multiplicado por 5, produzindo um número entre 0 e 5. Depois, o programa soma 5, fazendo com que a nota final fique entre: 5.0 e 10.0

---

**11. O que significa private em alguns pontos do código?**

`private` é um modificador de acesso. Ele serve para limitar quem pode acessar um atributo ou método.

No código, ele aparece por exemplo aqui:

```
private String name;  
private String id;  
private double grade;  
```

Isso significa que:
- os atributos `name`, `id` e `grade` só podem ser acessados diretamente dentro da própria classe `Student`.

**Exemplo**

Dentro da classe funciona:

  `this.grade = grade;`

Mas fora da classe, não podemos fazer:

  `student.grade`

porque o atributo é privado.

Para acessar a nota o código usa:

  `student.getGrade()`

porque o método `getGrade()` é público.


## Parte exploratória

Escolhi o projeto open source JabRef. O JabRef é um software desenvolvido em Java para gerenciamento de referências bibliográficas acadêmicas.

Link do projeto:
https://github.com/JabRef/jabref

Classe analisada: https://github.com/JabRef/jabref/blob/main/jabgui/src/main/java/org/jabref/cli/ArgumentProcessor.java

Trecho observado:

```java
package org.jabref.cli;

import java.util.ArrayList;
import java.util.List;

import org.jabref.gui.preferences.GuiPreferences;
import org.jabref.logic.UiCommand;
import org.jabref.logic.util.strings.StringUtil;

import picocli.CommandLine;

public class ArgumentProcessor {

    public enum Mode { INITIAL_START, REMOTE_START }

    private final Mode startupMode;
    private final GuiPreferences preferences;
    private final GuiCommandLine guiCli;
    private final CommandLine cli;

    private final List<UiCommand> uiCommands = new ArrayList<>();
    private boolean guiNeeded = true;

    public ArgumentProcessor(String[] args,
                             Mode startupMode,
                             GuiPreferences preferences) {
        this.startupMode = startupMode;
        this.preferences = preferences;
        this.guiCli = new GuiCommandLine();

        cli = new CommandLine(this.guiCli);
        cli.parseArgs(args);
    }

    public List<UiCommand> processArguments() {
        uiCommands.clear();
        guiNeeded = true;

        if (guiCli.blank) {
            uiCommands.add(new UiCommand.BlankWorkspace());
            return uiCommands;
        }

        if (StringUtil.isNotBlank(guiCli.jumpToKey)) {
            uiCommands.add(new UiCommand.SelectEntryKeys(List.of(guiCli.jumpToKey)));
        }

        return uiCommands;
    }
}
```

- Ao analisar a classe `ArgumentProcessor`, entendi que o programa parece processar comandos digitados pelo usuário no terminal, como abrir arquivos e importar preferências. Percebi a definição de classes usando `public class`, a utilização de atributos privados com `private` e a criação de objetos usando `new`. Também identifiquei listas utilizando `List` e `ArrayList`, semelhantes às usadas no exercício da aula com Student.
- Tive dificuldade principalmente com as bibliotecas externas importadas pelo projeto, como UiCommand. Também não entendi completamente como todas as classes do sistema se conectam, porque o projeto é muito grande e possui muitas dependências.

## Referências

- [Material da aula sobre programação orientada a objetos](https://liascript.github.io/course/?https://raw.githubusercontent.com/AndreaInfUFSM/elc117-2026a/main/classes/19/README.md#1)
- [Compilação e execução](https://cursos.alura.com.br/forum/topico-compile-e-rode-seu-primeiro-programa-java-272299)
- [Métodos: módulos de programa em Java](https://www.devmedia.com.br/metodos-modulos-de-programa-em-java/26771)
- [Modificadores de Acesso em Java](https://www.devmedia.com.br/modificadores-de-acesso-em-java/18822)
