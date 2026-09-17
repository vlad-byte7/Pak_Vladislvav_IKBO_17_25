## Задание 1: 
grep -o '^[^:]*' /etc/passwd | sort
## Задание 2:
grep -v '^#' /etc/protocols | sort -k2,2nr | head -n 5 | awk '{print $2, $1}'
