ntee
====

Portable Unix shell command `tee`, with some extras - read from standard input and write to standard output and files.

## TL;DR

`gulp.dest()` in middle of a pipe? NPM scripts can do as well:

```json
{
  "scripts": {
    "less": "lessc main.less | postcss --use autoprefixer | ntee main.css |  cleancss > main.min.css"
  }
}

```

## Install

```bash
$ [sudo] npm install -g ntee
```

## Check

```bash
$ ntee --help
```

## Use

```
ntee [OPTIONS] [FILE]

Options:
  -a, --append           append to the given FILEs, do not overwrite
  -i, --ignore-interrupts ignore interrupt signals
  -s, --suppress         do NOT output to stdout
  -v, --version          Display the current version
  -h, --help             Display help and usage details
```


```bash
$ whoami | ntee file1.txt file2.txt
```

Will print current user to stdout and also to `file1.txt` and `file2.txt`. Note that if these files already exist, they will be overwritten. Use `-a`/`--append` to avoid it, just like you would do with Richard Stallman's `tee`:

```bash
$ whoami | ntee -a i-wont-be-overwritten.txt
```

`-i`/`--ignore-interrupts` will prevent <kbd>CTRL</kbd>+<kbd>C</kbd> from killing `ntee`. Won't work on windows.

I also added an `-s`/`--suppress` option to suppress output to stdout. This meant to be used on npm scripts:

```bash
$ echo "Nothing will be shown in screen" | ntee -s but-it-will-be-saved-here.txt
```

You can always pipe:

```bash
cat long.log | sort | ntee sorted.log | head
```

## License

[MIT](./README.md) ♥
