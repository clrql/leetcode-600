
  # restore-ip-addresses

  ```golang
  func restoreIpAddresses(s string) []string {
    var result []string
    var currentIP []string
    backtrack(0, s, &currentIP, &result)
    return result
}

func backtrack(start int, s string, currentIP *[]string, result *[]string) {
    if start == len(s) && len(*currentIP) == 4 {
        *result = append(*result, strings.Join(*currentIP, "."))
        return
    }

    if len(*currentIP) == 4 || len(s)-start > (4-len(*currentIP))*3 {
        return
    }

    for i := 1; i <= 3 && start+i <= len(s); i++ {
        substring := s[start : start+i]
        num, _ := strconv.Atoi(substring)

        if num <= 255 {
            *currentIP = append(*currentIP, substring)
            backtrack(start+i, s, currentIP, result)
            *currentIP = (*currentIP)[:len(*currentIP)-1]
        }

        if s[start] == '0' {
            break
        }
    }
}

  ```
  