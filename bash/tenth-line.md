
  # tenth-line

  ```bash
  # Read from the file file.txt and output the tenth line to stdout.

filename="file.txt"
line_number=10

# Check if the file has at least 10 lines
if [ $(wc -l < "$filename") -ge $line_number ]; then
    # Print the 10th line using head and tail commands
    head -n $line_number "$filename" | tail -n 1
fi
  ```
  