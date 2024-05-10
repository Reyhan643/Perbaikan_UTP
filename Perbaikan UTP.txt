import java.util.Scanner;
import java.time.LocalDate;

public class PemesananTiketKonser {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Selamat datang di Pemesanan Tiket Konser!");

        // Dapatkan nama pengguna
        System.out.print("Masukkan nama Anda: ");
        String nama = scanner.nextLine();

        // Dapatkan tanggal pesanan
        LocalDate tanggalPesanan = LocalDate.now();

        // Tampilkan pilihan tiket
        System.out.println("\nPilih jenis tiket Anda:");
        System.out.println("1. CAT 8");
        System.out.println("2. CAT 1");
        System.out.println("3. FESTIVAL");
        System.out.println("4. VIP");
        System.out.println("5. UNLIMITED EXPERIENCE");
        System.out.print("Masukkan pilihan Anda: ");

        int pilihan = scanner.nextInt();
        scanner.nextLine(); // Konsumsi karakter baris baru

        // Validasi pilihan tiket
        while (pilihan < 1 || pilihan > 5) {
            System.out.print("Pilihan tidak valid. Harap masukkan angka antara 1 dan 5: ");
            pilihan = scanner.nextInt();
            scanner.nextLine();
        }

        // Hitung harga tiket berdasarkan pilihan
        double hargaTiket = 0;
        switch (pilihan) {
            case 1:
                hargaTiket = 100000;
                break;
            case 2:
                hargaTiket = 200000;
                break;
            case 3:
                hargaTiket = 300000;
                break;
            case 4:
                hargaTiket = 500000;
                break;
            case 5:
                hargaTiket = 1000000;
                break;
        }

        // Ubah harga ke dalam USD
        double kursUSD = 14000; // Kurs saat ini, ubah sesuai dengan kurs aktual
        double hargaUSD = hargaTiket / kursUSD;
        
        // Format harga menjadi USD
        String formattedHargaUSD = formatHargaUSD(hargaUSD);

        // Generate kode booking
        String kodeBooking = generateBookingCode();

        // Tampilkan konfirmasi pesanan
        System.out.println("\n--- Detail Pesanan ---");
        System.out.println("Nama: " + nama);
        System.out.println("Tanggal Pesanan: " + tanggalPesanan);
        System.out.println("Kode Booking: " + kodeBooking);
        System.out.println("Jenis Tiket: " + getTicketTypeName(pilihan));
        System.out.println("Harga Total: " + formattedHargaUSD);

        System.out.println("\nTerima kasih atas pesanan Anda!");

        // Tutup scanner setelah selesai menggunakannya
        scanner.close();
    }

    private static String generateBookingCode() {
        String chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
        StringBuilder code = new StringBuilder();
        for (int i = 0; i < 8; i++) {
            code.append(chars.charAt((int) (Math.random() * chars.length())));
        }
        return code.toString();
    }

    private static String getTicketTypeName(int pilihan) {
        switch (pilihan) {
            case 1:
                return "CAT 8";
            case 2:
                return "CAT 1";
            case 3:
                return "FESTIVAL";
            case 4:
                return "VIP";
            case 5:
                return "UNLIMITED EXPERIENCE";
            default:
                return "Tidak Dikenal";
        }
    }
    
    private static String formatHargaUSD(double hargaUSD) {
        if (hargaUSD >= 1000) {
            return String.format("%.2e USD", hargaUSD);
        } else {
            return String.format("%.2f USD", hargaUSD);
        }
    }
}
