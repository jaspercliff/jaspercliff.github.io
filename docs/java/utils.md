# javap
`javap` 是 Java 的类文件反编译器。它是 Java Development Kit (JDK) 的一部分，用于反编译并打印 `.class` 文件的结构信息到控制台。
`javap` 提供了类文件中的类定义的各种详细信息，包括构造函数、方法、字段和字节码（如果使用 `-c` 选项）。

使用 `javap` 时，可以带上不同的参数来获取不同级别的信息。这里是一些常见的 `javap` 选项：

- `-c`：反编译所提供类的字节码。
- `-p` 或 `-private`：显示所有类成员，包括私有的。
- `-verbose`：输出附加信息，例如类文件的版本、常量池、方法参数。
- `-s`：输出内部类型签名。
- `-l`：输出行号和本地变量表。

要使用 `javap` 查看 `OuterClass` 或其内部类 `InnerClass1` 的详细信息，你会在命令行中输入以下命令：

```bash
javap -c -verbose -p com.jasper.classDemo.OuterClass
```

或者对于内部类：

```bash
javap -c -verbose -p com.jasper.classDemo.OuterClass$InnerClass1
```

在运行这些命令之前，需要确保 `.class` 文件的路径在类路径上，或者在命令中提供正确的路径。这将输出对应类的详细信息，包括任何合成构造函数或方法。

如果你尝试使用 `javap` 并遇到了问题，例如命令找不到或类文件找不到，你需要检查你的 JDK 安装以及类文件的路径是否正确。在 `javap` 命令中使用的类名应该是完全限定名（包括包名）。