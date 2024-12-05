---
sidebar_position: 11
---

# Program Libraries

Libraries make it easy to use pre-made programs in the sandbox.

```py
    if !FileAccess.file_exists("res://luajit.elf"):
        var buffer = Sandbox.download_program("luajit")
        fa = FileAccess.open("res://luajit.elf", FileAccess.WRITE)
        fa.store_buffer(buffer)
        fa.close()

    var luajit = Node.new()
    luajit.set_script(load("res://luajit.elf"))

    luajit.add_function("test", func(name): return "Test " + str(name) + " called!")
    luajit.add_function("add", func(a, b): return a + b)

    luajit.run("""
    print(test(1))
    print(add(333, 666))
    function fib(n, acc, prev)
        if (n < 1) then
            return acc
        else
            return fib(n - 1, prev + acc, acc)
        end
    end
    print("The 500th fibonacci number is " .. fib(500, 0, 1))
    """)
```

## Godot Sandbox Programs

There is [a repository with pre-made programs](https://github.com/libriscv/godot-sandbox-programs).

You can find [the latest release here](https://github.com/libriscv/godot-sandbox-programs/releases/latest). The latest release is used by `Sandbox.download_program(name)`.
