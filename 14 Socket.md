# 聊天

## 服务器端

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Net;
using System.Net.Sockets;
using System.Threading;
//Tcp协议  服务器端
namespace ServerSocket
{
    class Program
    {
        public static List<ClientSocket> cSocketList = new List<ClientSocket>();
        static void Main(string[] args)
        {

            //创建监听连接的Socket
            Socket serverSocket = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
            Console.WriteLine("创建服务器");
            IPAddress address = IPAddress.Parse("192.168.2.107");
            IPEndPoint point = new IPEndPoint(address, 12345);
            //绑定服务器IP和端口
            serverSocket.Bind(point);
            Console.WriteLine("绑定IP和端口");
            //设定监听队列人数
            serverSocket.Listen(30);
            Console.WriteLine("开始监听");
            while(true)
            {
                //等待用户连接，如果用户连接则返回一个与用户通讯的Socket
                Socket newsocket = serverSocket.Accept();
                if(newsocket != null)
                {
                    Console.WriteLine("有一个客户端连接成功..");
                    Console.WriteLine("客户端IP：" + (IPEndPoint)newsocket.LocalEndPoint);
                }
                ClientSocket CSocket = new ClientSocket(newsocket);
                //将新创建的Socket对象添加列表中
                cSocketList.Add(CSocket);
                
            }
        }
        //用来广播消息
        public static void BroadCastMessage(string msg)
        {
            var newSocketList = new List<ClientSocket>();
            for (int i = 0; i < cSocketList.Count; i++)
            {
                if (cSocketList[i].isConnent)
                {
                    cSocketList[i].SendMessage(msg);
                }
                else
                {
                    newSocketList.Add(cSocketList[i]);
                }
            }
            //删除所有离线客户端
            for (int i = 0; i < newSocketList.Count; i++)
			{
                cSocketList.Remove(newSocketList[i]);
			}
        }
    }
    //服务器用来和客户端交互的Socket类
    public class ClientSocket
    {
        private Socket tcpS2CSocket;

        public bool isConnent
        {
            get { return tcpS2CSocket.Connected; }
        }
        public ClientSocket(Socket socket)
        {
            this.tcpS2CSocket = socket;
            //开启线程接收客户端发送过来的消息
            thread = new Thread(ReceiveMessage);
            thread.Start();
        }
        private Thread thread;
        //接收客户端消息
        //接收消息
        private void ReceiveMessage()
        {
            //用来判断客户端的socket是否还在连接状态
            while (true)
            {
                if(tcpS2CSocket.Poll(10,SelectMode.SelectRead))
                {
                    tcpS2CSocket.Close();
                    break;
                }
            
                byte[] bytetemps = new byte[2048];
                //获得该消息的长度
                int length = tcpS2CSocket.Receive(bytetemps);
                string msg = Encoding.UTF8.GetString(bytetemps, 0, length);
                Console.WriteLine("接收到的客户端消息：" + msg);
                //广播消息
                Program.BroadCastMessage(msg);
            }
        }
        //发送消息
        public void SendMessage(string message)
        {
           
                byte[] bytes = Encoding.UTF8.GetBytes(message);
                tcpS2CSocket.Send(bytes);
                Console.WriteLine("客户端向服务器发送消息：" + message);
        }
    }
}
```

## 客户端
```C#
using UnityEngine;
using System.Collections;
using System.Net;
using System.Net.Sockets;
using UnityEngine.UI;
using System.Text;
using System.Threading;
public class SocketClientChat : MonoBehaviour {

    public InputField inputfield;
    public Button buttonSend;
    public Text chattext;
    public Socket ClientSocket;
    
    public Thread thread;
   void Awake()
    {
        inputfield = transform.Find("Panel/InputFieldChat").GetComponent<InputField>();
        buttonSend = transform.Find("Panel/SendBut").GetComponent<Button>();
        buttonSend.onClick.AddListener(C2S_SendMessage);
        chattext = transform.Find("Panel/ChatText").GetComponent<Text>();
    }
	void Start () {
        //创建与服务端连接的Socket（负责接收和发送消息）
        ClientSocket = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
        //连接服务器
        IPAddress ipaddress = IPAddress.Parse("192.168.2.107");
        int port = 12345;
        IPEndPoint point = new IPEndPoint(ipaddress, port);
        //连接服务器
        ClientSocket.Connect(point);
        print("客户端请求连接服务器。。。。");
        thread = new Thread (ReceiveMessage);
        thread.Start();
	}
    //向服务端发送消息
    public void C2S_SendMessage()
    {
        byte[] bytes = Encoding.UTF8.GetBytes(inputfield.text);
        ClientSocket.Send(bytes);
        print("客户端向服务器发送消息：" + inputfield.text);
        inputfield.text = "";
    }
    public string message;
    //接收服务器发过来的消息
    private void ReceiveMessage()
    {
        while (true)
        {
            if(ClientSocket.Connected == false)
            {
                break;
            }
            byte[] bytetemp = new byte[2048];

            int length = ClientSocket.Receive(bytetemp);
            message = Encoding.UTF8.GetString(bytetemp, 0, length);
            print("接收到服务器的消息：" + message);
        }
    }
	
	// Update is called once per frame
	void Update () {
        if(message != null && message != "")
        {
            ShowText(message);
            message = "";
        }
	}
    void ShowText(string message)
    {
        chattext.text += message + "\n";
    }
}
```





