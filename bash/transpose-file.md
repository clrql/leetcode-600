
  # transpose-file

  ```bash
  # Read from the file file.txt and print its transposed content to stdout.

transpose=$(awk '{ for(i=1; i<=NF; i++) { a[i,NR]=$i } } END { for(i=1; i<=NF; i++) { for(j=1; j<=NR; j++) { printf "%s%s", a[i,j], (j==NR ? RS : FS) } } }' file.txt)

echo "$transpose"
  ```
  