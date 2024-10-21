import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.util.Scanner;

public class convertidorDeMoneda {
    public static void main(String[] args) throws IOException, InterruptedException {
        Scanner scanner = new Scanner(System.in);


        System.out.println("Ingrese la moneda a convertir(EUR,USD,PESO COLOMBIANO etc.):");
        String monedaOrigen = scanner.nextLine().toUpperCase();;
        System.out.println("Ingrese la moneda que desea hacer el cambio(EUR,USD,PESO COLOMBIANO etc.):");
        String monedaDestino = scanner.nextLine().toUpperCase();
        System.out.println("Digite monto que desea convertir");
        double monto = scanner.nextDouble();
        //double tipoDeCambio = obtenerTipoDeCambio(monedaOrigen,monedaDestino);
        //double resultado = monto * tipoDeCambio;
        //System.out.println(monto + "" + monedaOrigen + " = " + resultado + "" + monedaDestino);
        try {
            double rate = obtenerTipoDeCambio(monedaOrigen, monedaDestino);
            double resultado = monto * rate;
            System.out.println(monto + " " + monedaOrigen + " = " + resultado + " " + monedaDestino);
        } catch (Exception e) {
            System.out.println("Error al obtener la tasa de cambio: " + e.getMessage());
        }

        scanner.close();
    }


    private static double obtenerTipoDeCambio(String monedaOrigen, String monedaDestino) throws IOException, InterruptedException {
        try {
            HttpClient client = HttpClient.newHttpClient();
            HttpRequest request = HttpRequest.newBuilder()
                    .uri(URI.create("https://v6.exchangerate-api.com/v6/6410eae163d702ec75891627/latest/COP" + monedaOrigen + "/" + monedaDestino))
                    .build();

            HttpResponse<String> response = client


                    .send(request, HttpResponse.BodyHandlers.ofString());
            if (response.statusCode() != 200) {
                throw new RuntimeException("Error en la respuesta de la API: " + response.statusCode());


            }
        } finally {

        }
            return 0;
            }

    private static void build() {
    }
}
