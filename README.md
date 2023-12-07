писят два
лвмаыщжоызщ
\q\AZWXESCDRTVFGBYHS`WECDRTVFHNUMJIO,KP.L
47
# duh




using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.IO;
using System.Security.Cryptography;

namespace _8
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {

        }

        private void button1_Click(object sender, EventArgs e)
        {
            try
            {
                using (FileStream fileStream = new ("TestData.txt", FileMode.OpenOrCreate))
    {
                    using (Aes aes = Aes.Create())
                    {
                        byte[] key =
                        {
                0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08,
                0x09, 0x10, 0x11, 0x12, 0x13, 0x14, 0x15, 0x16
            };
                        aes.Key = key;

                        byte[] iv = aes.IV;
                        fileStream.Write(iv, 0, iv.Length);

                        using (CryptoStream cryptoStream = new (
                            fileStream,
                            aes.CreateEncryptor(),
                            CryptoStreamMode.Write))
            {
                            // By default, the StreamWriter uses UTF-8 encoding.
                            // To change the text encoding, pass the desired encoding as the second parameter.
                            // For example, new StreamWriter(cryptoStream, Encoding.Unicode).
                            using (StreamWriter encryptWriter = new (cryptoStream))
                            {
                                encryptWriter.WriteLine("Hello World!");
                            }
                        }
                    }
                }

                Console.WriteLine("The file was encrypted.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"The encryption failed. {ex}");
            }
        }
    }
}

