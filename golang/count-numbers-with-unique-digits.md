
  # count-numbers-with-unique-digits

  ```golang
  func countNumbersWithUniqueDigits(n int) int {
    if n == 0 {
		return 1
	} else if n == 1 {
		return 10
	}

	// Inicializamos el resultado con 10 (números de un solo dígito).
	result := 10
	// El primer dígito tiene 9 opciones (1-9).
	uniqueDigits := 9
	// Inicializamos el número de opciones disponibles para el segundo dígito.
	availableDigits := 9

	for i := 2; i <= n; i++ {
		// Multiplicamos el número de opciones únicas por las opciones disponibles y actualizamos el resultado.
		uniqueDigits *= availableDigits
		result += uniqueDigits
		// Reducimos el número de opciones disponibles para el siguiente dígito.
		availableDigits--
	}

	return result
}
  ```
  