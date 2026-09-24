## Задание 1: 
grep -o '^[^:]*' /etc/passwd | sort
## Задание 2:
grep -v '^#' /etc/protocols | sort -k2,2nr | head -n 5 | awk '{print $2, $1}'
## Задание 3
#!/bin/bash

text="$1"

length=${#text}
line=$(printf '%*s' $((length + 2)) '' | tr ' ' '-')

echo "+$line+"
echo "| $text |"
echo "+$line+"
## Задание 4
#!/bin/bash

grep -o '\b[A-Za-z_][A-Za-z0-9_]*\b' "$1" | sort -u
## Задание 5
#!/bin/bash

chmod +x "$1"
sudo cp "$1" /usr/local/bin/
## Задание 6
    #!/bin/bash

    for file in *.c *.js *.py; do
        [ -e "$file" ] || continue
        
        first_line=$(head -n 1 "$file")
        
        case "$file" in
            *.c|*.js)
                if echo "$first_line" | grep -Eq '^[[:space:]]*(//|/\*)'; then
                    echo "$file: комментарий есть"
                else
                    echo "$file: комментария нет"
                fi
                ;;
            *.py)
                if echo "$first_line" | grep -Eq '^[[:space:]]*#'; then
                    echo "$file: комментарий есть"
                else
                    echo "$file: комментария нет"
                fi
                ;;
        esac
    done
## Задание 7
#!/bin/bash

if [ -z "$1" ]; then
    echo "Укажите путь"
    exit 1
fi

find "$1" -type f -exec sha256sum {} + | sort | uniq -w 64 -D
## Задание 8
#!/bin/bash

find . -maxdepth 1 -type f -name "*.$1" -print0 | tar --null -cf archive.tar -T -
## Задание 9
#!/bin/bash

if [ -z "$1" ] || [ -z "$2" ]; then
    echo "Укажите входной и выходной файлы"
    exit 1
fi

sed 's/    /\t/g' "$1" > "$2"
## Задание 10
#!/bin/bash

find "$1" -maxdepth 1 -type f -empty -print
