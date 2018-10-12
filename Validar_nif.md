* Como validar NIF
```Java
package validarNIF;

import java.util.*;

public class ValidaNif {
	public static Scanner teclado = new Scanner(System.in);

	public static boolean validarLetraYNumero(String nif) {

		boolean comprueboLetra = false;
		boolean esDigito = false;
		boolean todoValido = false;
		int letra = 0;

		if (nif.length() == 9 && Character.isLetter(nif.charAt(nif.length() - 1))) {

			comprueboLetra = true;
		}
		for (int i = 0; i < nif.length() - 1; i++) {

			if (Character.isDigit(nif.charAt(i))) {
				// saber si el caracter es un número
				esDigito = true;
				break;
			}

		}
		if (comprueboLetra == true && esDigito == true) {
			todoValido = true;
		}

		return todoValido;
	}

	public static boolean validarNif(String nif) {
		String[] letraNif = { "T", "R", "W", "A", "G", "M", "Y", "F", "P", "D", "X", "B", "N", "J", "Z", "S", "Q", "V",
				"H", "L", "C", "K", "E" };
		boolean esValido = false;
		int numero = Integer.parseInt(nif.substring(0, nif.length() - 2));
		numero = numero % 23;

		for (int i = 0; i < letraNif.length; i++) {

			if (nif.charAt(nif.length() - 1) == letraNif[i].charAt(0)) {
				esValido = true;
			}
		}

		return esValido;
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		String nif = "";

		System.out.println("Introduzca el NIF");
		nif = teclado.nextLine().trim().replaceAll("\\s", "");

		if (validarLetraYNumero(nif) == true && validarNif(nif) == true) {
			System.out.println("El NIF es válido, y la parte númerica es: " + nif.substring(0, nif.length() -1));
		} else {
			System.out.println("El NIF introducido no es válido.");
		}

	}

}
```
