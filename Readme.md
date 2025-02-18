# Igniton file
 Step Membuat Igntion file, kalian bisa melihat pada ./templete pada directory tersebut terdapat file mentah untuk membuat file igntion. Untuk hasilnya kita bisa lihat pada directory ./example. Bagaimana kita menulis file ignition atau menambah feature tertenu? untuk refrence bisa diliha pada [dokumentasi_berikut](https://coreos.github.io/ignition/examples/)

 Disin kita akan membuat igntion dari template yang tersedia

 ```
 git clone https://github.com/galihtw04/coreos-ign.git
 cd coreos-ign/
 ```

## Generate

  ### Generate Network

  Sesuaikan dengan Network Enviroment Kalian

  ```sh
  # Sesuaikan degan network Enviroment kalian
  vim Network_template.conf
  ```

  Genereate Network dan encrypt menggunakan base64

  ```sh
  # Encrypt
  base64 -w0 Network_template.conf > node01.txt
  ```

  ### Generate Password

  Berikutnya kita akan generate Password, untuk generate password kita menggunakan openssl bukan bas64

  ```sh
  openssl passwd -6 "P@ssw0rd123" > password.txt
  ```

## Configuration Ignition File

   Karena sudah ada bahan-bahan untuk membuat igntion file, kita sekarang siap untuk membuat ignition file.

   ```sh
   vim ignitionfile.json
   ```
   > masukan sesuai dengan bahan yang ada

## Result
   hasilnya akan seperti ini

  ```json
  {
    "ignition": {
      "version": "3.3.0"
    },
    "storage": {
      "files": [
        {
          "path": "/etc/hostname",
          "mode": 420,
          "contents": {
            "source": "data:,nodename01"
          }
        },
        {
          "path": "/etc/NetworkManager/system-connections/enp5s0.nmconnection",
          "mode": 384,
          "overwrite": false,
          "contents": {
            "source": "data:text/plain;charset=utf-8;base64,  W2Nvbm5lY3Rpb25dCmlkPSdXaXJlZCBjb25uZWN0aW9uIDEubm1jb25uZWN0aW9uJwp0eXBlPWV0aGVybmV0CmF1dG9jb25uZWN0PXRydWUKaW50ZXJmYWNlLW5hbWU9ZW5wNXMwCgpbZXRoZXJuZXRdCm1hYy1hZGRyZXNzLWJs  YWNrbGlzdD0KCltpcHY0XQptZXRob2Q9bWFudWFsCmFkZHJlc3Nlcz0xMC4zMS4wLjEwNS8yNApnYXRld2F5PTEwLjMxLjAuMQpkbnM9OC44LjguODs4LjguNC40OwpkbnMtc2VhcmNoPQoKW2lwdjZdCm1ldGhvZD1pZ25vcmUK  Cltwcm94eV0KCg=="
          }
        }
      ]
    },
    "passwd": {
      "users": [
        {
          "name": "student",
          "passwordHash": "$6$AoLLZ8r/h5fc0wnC$WLN/Ye5liNt4HrLZDCWWNoWKQWj9GvrEZ.2c80JKvPMQ/eu.EH7DoorZqMLrqULpg2tmcUEPk5LRhGMh0D.Vd/",
          "groups": ["sudo"],
          "shell": "/bin/bash",
          "sshAuthorizedKeys": [
            "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5A..."
          ]
        }
      ]
    },
    "systemd": {
      "units": [
        {
          "name": "systemd-networkd.service",
          "enabled": true
        }
      ]
    }
  }   
  ```

  > Untuk mode file ini tidak menggunakan permission seperti chmod biasanya, untuk mode ini kita di tulis sebagai binner

| Number | Permission       | Symbolic Representation |
|--------|-----------------|-------------------------|
| 0      | No permission   | ---                     |
| 1      | Execute (`x`)   | --x                     |
| 2      | Write (`w`)     | -w-                     |
| 3      | Write + Execute (`wx`) | -wx          |
| 4      | Read (`r`)      | r--                     |
| 5      | Read + Execute (`rx`) | r-x          |
| 6      | Read + Write (`rw`) | rw-              |
| 7      | Read + Write + Execute (`rwx`) | rwx  |
