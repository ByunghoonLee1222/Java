# Network

* TCP

  * 하나의 스트림

  * HTTP

* UDP

  * 다중연결

#### Client

---

* 소켓 생성후  IO 연결

#### Server

---

**port**

* 0~65535
* 0~1023 : System Port (http : 80)
* 소켓 생성후 accept 계속 수신

```java
	public class BookClient extends Thread {
		public void run() {
			Socket s = null;
			ObjectOutputStream oos = null;
			try {
				s = new Socket("localhost", 3619);
				oos = new ObjectOutputStream(s.getOutputStream());
				oos.writeObject(books);
			} catch (Exception e) {
				e.printStackTrace();
			} finally {
				IOUtill.close(oos);
				IOUtill.close(s);
			}
		}
	}

	@Override
	public void send() {
		new BookClient().start();
	}

////////////////////////////////////////server///////////////////////
	public static void main(String[] args) {

		ServerSocket ss = null;
		try {
			ss = new ServerSocket(5431);
			System.out.println("ProductServer start......");
			while (true) {
				Socket s = ss.accept();
				String fileName = s.getInetAddress().toString().substring(1) + "Obeject.txt";
				System.out.println("클라이언트" + s.getInetAddress() + "접속");
				FileOutputStream fos = null;
				ObjectOutputStream oos = null;
				ObjectInputStream ois = null;
				try {
					// 네트웍으로 부터 데이터 전송 받을 스트림
					ois = new ObjectInputStream(s.getInputStream());
					fos = new FileOutputStream(fileName);
					// 파일에 출력할 스트림
					oos = new ObjectOutputStream(fos);
					// 네트워크로 부터 입력 받은 데이터를 바로 출력
					Object ob = ois.readObject();
					ArrayList<Product> tv = (ArrayList) ob;
					for (Product b : tv) {
						System.out.println(b);
					}
					System.out.println("TV 출력 완료");
					Object ob2 = ois.readObject();
					ArrayList<Product> refri = (ArrayList) ob2;
					for (Product b : refri) {
						System.out.println(b);
					}
					System.out.println("Refrigerator 출력 완료");
				} catch (Exception e) {
					e.printStackTrace();
				} finally {
					IOUtill.close(oos);
					IOUtill.close(fos);
					IOUtill.close(ois);
					IOUtill.close(s);
				}
			}
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			IOUtill.close(ss);
		}
	}

```

