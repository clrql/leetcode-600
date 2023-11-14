
  # simplify-path

  ```golang
  func simplifyPath(path string) string {
    dirs := strings.Split(path, "/")
    stack := make([]string, 0, len(dirs))
    
    for _, dir := range dirs {
        if dir == "." || dir == "" {
            continue
        }
        if dir == ".." {
            if len(stack) > 0 {
                stack = stack[:len(stack)-1]
            }
        } else {
            stack = append(stack, dir)
        }
    }
    
    if len(stack) == 0 {
        return "/"
    }
    
    return "/" + strings.Join(stack, "/")
}
  ```
  