# Pertemuan Kelima - Membuat Aplikasi CRUD dengan Java Swing dan JDBC
Penugasan Mata Kuliah PBO pertemuan kelima kali ini yaitu membuat aplikasi CRUD (Create, Read, Update, Delete) menggunakan Java Swing untuk membuat aplikasi berbasis GUI, serta mengelola data menggunakan JDBC (Java Database Connectivity) agar terhubung dengan database.

---
## Koneksi JDBC
Mengkoneksikan aplikasi Java menggunakan JDBC (Java Database Connectivity) agar terhubung dengan basis data.
### Langkah-langkah
1. Buat Database dan Tabel: Buat database baru dan tabel yang diperlukan di server database.
2. Tambahkan Driver JDBC ke Proyek: Menambahkan driver JDBC yang sesuai dan membuat objek `Connection` menggunakan `Driver`.
3. Buat Koneksi JDBC: Buat kelas Java yang mengatur koneksi ke database menggunakan `DriverManager.getConnection()` dengan URL, username, dan password.
4. Uji Koneksi: Buat kelas utama untuk menguji koneksi dan pastikan dapat terhubung ke database.

### Contoh
````java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

    Connection conn;
    Statement stmt;
    PreparedStatement pstmt = null;

    String driver = "org.postgresql.Driver";
    String koneksi = "jdbc:postgresql://localhost:5432/PBO";
    String user = "postgres";
    String password = "kuanlinee";
    InputStreamReader inputStreamReader = new InputStreamReader(System.in);
    BufferedReader input = new BufferedReader(inputStreamReader);
````
---
## DbSiswa
Buatlah kelas `DbSiswa` yang berfungsi untuk menyediakan method untuk memproses hasil dari query SQL dan menampilkannya dalam bentuk tabel di aplikasi GUI berbasis Java Swing. Metode `resultSetToTableModel(ResultSet rs)` adalah salah satu fungsi utama di dalam kelas ini. Fungsi ini mengambil hasil query dari database (dalam bentuk `ResultSet`) dan mengonversinya menjadi `TableModel` yang dapat digunakan untuk menampilkan data di komponen GUI seperti `JTable`.
### Contoh
````java
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.util.Vector;
import javax.swing.table.DefaultTableModel;
import javax.swing.table.TableModel;

  public class DbSiswa {
      public static TableModel resultSetToTableModel(ResultSet rs) {
          try {
              ResultSetMetaData metaData = rs.getMetaData();
              int numberOfColumns = metaData.getColumnCount();
              Vector columnNames = new Vector();
  
              // Get the column names
              for (int column = 0; column < numberOfColumns; column++) {
                  columnNames.addElement(metaData.getColumnLabel(column + 1));
              }
  
              // Get all rows.
              Vector rows = new Vector();
  
              while (rs.next()) {
                  Vector newRow = new Vector();
  
                  for (int i = 1; i <= numberOfColumns; i++) {
                      newRow.addElement(rs.getObject(i));
                  }
  
                  rows.addElement(newRow);
              }
  
              return new DefaultTableModel(rows, columnNames);
          } catch (Exception e) {
              e.printStackTrace();
              return null;
          }
      }
  }
````
---
## Java Swing
Java Swing adalah alat yang digunakan untuk membuat antarmuka pengguna (GUI) dalam aplikasi Java. Dalam Java Swing menyediakan berbagai elemen seperti tombol, label, tabel, dan daftar, yang bisa kamu gunakan untuk membuat tampilan.

---
## CRUD
CRUD adalah singkatan dari Create, Read, Update, dan Delete. Ini adalah empat operasi dasar yang sering digunakan dalam aplikasi untuk mengelola data. CRUD adalah dasar dari banyak aplikasi, terutama yang berhubungan dengan database, karena membantu dalam mengelola data dengan cara yang terstruktur.
1. Create (Buat): Menambahkan data baru ke dalam sistem.
2. Read (Baca): Mengambil dan menampilkan data yang sudah ada.
3. Update (Perbarui): Mengubah atau memperbarui data yang sudah ada.
4. Delete (Hapus): Menghapus data dari sistem.

---
