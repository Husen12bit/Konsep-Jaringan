
# TUGAS KONSEP JARINGAN MINGGU KE-12

---

![Image](https://github.com/user-attachments/assets/838b068c-4d85-452a-aca6-352d279fbd3f)

---

#### Dosen Pengampu :
**Muhammad Robihul Mufid S.ST, M.TR.Kom**

#### Disusun oleh :
**Muhammad Abdullah Husaini**
**(3214521030)**
D3-LA IT-A

---

## PYTHON FOR HACKING


**TENTANG TCP**

TCP (Transmission Control Protocol) adalah protokol connection-oriented dan reliable yang beroperasi pada lapisan Transport (Layer 4) dari model OSI. Fungsinya adalah untuk memastikan pengiriman data yang utuh, terurut, dan bebas kesalahan antara dua aplikasi yang berjalan di host yang berbeda melalui jaringan yang mungkin tidak andal.
Cara Kerja
1.	Three-Way Handshake:
- SYN (Synchronize): Pengirim (Client) mengirimkan segmen SYN ke penerima (Server) untuk memulai koneksi.
- SYN-ACK (Synchronize-Acknowledge): Server merespons dengan SYN untuk menerima koneksi dan ACK untuk mengkonfirmasi SYN dari Client.
- ACK (Acknowledge): Client merespons dengan ACK untuk mengkonfirmasi SYN-ACK dari Server. Koneksi terjalin.
2.	Data Transfer: Data aplikasi dipecah menjadi segmen-segmen TCP, diberi nomor urut, dan dikirim. Penerima membalas dengan ACK.
3.	Four-Way Handshake (Connection Termination):
- FIN (Finish): Salah satu pihak (seperti, Client) mengirimkan FIN untuk mengakhiri transmisi data dari sisinya.
- ACK: Pihak lain (Server) membalas dengan ACK.
- FIN: Server juga mengirimkan FIN ketika selesai mengirim datanya.
- ACK: Client membalas dengan ACK. Koneksi terputus sepenuhnya.

**CODE**

Client.py

    import socket
    
    if __name__ == "__main__" :
        ip = "127.0.0.1"
        port = 1234
    
        server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        server.connect((ip, port))
    
        string = input("Enter string: ")
        server.send(bytes(string, "utf-8"))
        buffer = server.recv(1024)
        buffer = buffer.decode("utf-8")
        print(f"Server: {buffer}")

Server.py

    import socket
    
    if __name__ == "__main__" :
        ip = "127.0.0.1"
        port = 1234
    
        server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        server.bind((ip, port))
        server.listen(5)
    
        while True:
            Client, address = server.accept()
            print(f"Connection Established - {address[0]}:{address[1]}")
    
            string = Client.recv(1024)
            string = string.decode("utf-8")
            string = string.upper()
            Client.send(bytes(string, "utf-8"))
            print(string)
            Client.close()

**HASIL**

<img width="613" height="152" alt="Screenshot 2025-11-18 195345" src="https://github.com/user-attachments/assets/82f092cd-169f-4e93-9238-92f1de01e5d5" />

<img width="591" height="115" alt="Screenshot 2025-11-18 195415" src="https://github.com/user-attachments/assets/72c5b8a3-c207-47f5-9300-a96f209e1413" />

---

---

**TENTANG UDP**

UDP (User Datagram Protocol) adalah protokol connectionless dan unreliable yang beroperasi pada lapisan Transport (Layer 4) dari model OSI. Fungsinya adalah untuk menyediakan transfer data yang cepat dengan overhead minimal, tanpa mekanisme untuk memastikan pengiriman, urutan, atau integritas data.
Cara Kerja:
1.	Aplikasi membuat data yang ingin dikirim.
2.	Data tersebut dibungkus dalam UDP datagram (menambahkan header UDP minimal).
3.	UDP datagram dikirim langsung ke IP layer untuk dikirimkan melalui jaringan.
4.	Tidak ada konfirmasi, tidak ada nomor urut, tidak ada jaminan.

**CODE**

UDPserver.py
    
    import socket
    
    localIP = "127.0.0.1"
    localPort = 9997
    buffer = 1024
    
    serverSocket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    serverSocket.bind((localIP, localPort))
    
    print("UDP server menyala")
    
    while (True):
        data = serverSocket.recvfrom(buffer)
        pesan = data[0]
        ip_address = data[1]
    
        print("Pesan dari Client: \"{}\"".format(pesan))
        print("IP Client: \"{}\"".format(ip_address))
    
        serverSocket.sendto(b"Selamat datang di UDP Server", ip_address)

UDPclient.py

    import socket
    
    Target_host = "127.0.0.1"
    target_port = 9997
    
    client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    
    client.sendto(b"hai",(Target_host, target_port))
    
    data, addr = client.recvfrom(4096)
    print("Pesan dari server: \"{}\"".format(data.decode()))
    
    client.close()

**HASIL**

<img width="577" height="117" alt="Screenshot 2025-11-18 212547" src="https://github.com/user-attachments/assets/56023f85-a801-4f96-ac2e-0a669f741adb" />

<img width="493" height="146" alt="Screenshot 2025-11-18 212824" src="https://github.com/user-attachments/assets/288cd71e-4b11-49bf-8add-14b96f1e1d7f" />

---

**PDF**

[LAPORAN RESMI PRAKT KONSEP JARINGAN 13 (Python for Hacking).pdf](https://github.com/user-attachments/files/23609125/LAPORAN.RESMI.PRAKT.KONSEP.JARINGAN.13.Python.for.Hacking.pdf)

---
