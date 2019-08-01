# I/O ( 파일 입출력)

* **NodeStream(I/O 하는 실제 대상)**

| 종류   | byte(모든데이터타입) I | byte(모든데이터타입) O | char(문자전용) I | char(문자전용)O |
| ------ | ---------------------- | ---------------------- | ---------------- | --------------- |
| 추상   | InputStream            | OutputStream           | Reader           | Writer          |
| file   | FileInputStream        | FileOutputStram        | FileReader       | FileWriter      |
| memory | ByteArrayInputStream   | ByteArrayInputStram    | CharArrayReader  | CharArraywriter |

#### 입력

* **int read()**; : Data 한개를 입력 받아 리턴
  * 읽지 못한경우 -1

* **int(읽은 Data 개수) read (byte[] buf) or int read(char[] buf)**
  * buf 크기만큼 입력 받기 (읽은 Data)
  * buf가 훨씬 빠르다

* **int read(byte[] buf, int off, int len)**

  * 읽을 것을 쌓아준다

  * 대체 함수(API) 존재 

#### 출력

* **void write(int data)** : 한개의 Data 출력
* **void write(byte[] buf)** : 배열의 모든 Data를 출력
* **void write(byte[] buf, int offset, int len)**: 배열의 offset부터 len개를 출력



### FileCopy

```java
public static void main(String[] args) 
    throws IOException {
		int read;
		FileOutputStream fos = null;
		try {
			fos = new FileOutputStream("res/keyboard1.txt");
			do {
				read = System.in.read();
				fos.write(read);
				if(read !='\n' && read!='\r') {
					System.out.println((char)read);	
				}
				
			}while(read !='x' && read != -1);
		} catch (Exception e) {
			e.printStackTrace();
		}finally {
			if(fos != null)
                try{fos.close();}catch(Exception e){}
		}
	}
////////////////////////////////////////
		FileReader fis = null;
		FileWriter fos = null;
		String readFile = "src/chapter10/FileCopy3.java";
//		String readFile = "c:/SSAFY/yellow.jpg";
	
	//	String writeFile="res/copy1.txt";
		String writeFile="res/copy3.java";
//		String writeFile="res/copy1.jpg";
		try {
			/**지정한 경로에 파일이 없으면 FileNotFoundException 발생*/
			fis =  new FileReader(readFile);
			/**출력할 파일이 경로에 없으면 파일을 생성한다.*/
			fos =  new FileWriter(writeFile);
			int read;
			char[] buf = new char[1024];
			
			while((read = fis.read(buf))!= -1) {
				fos.write(read);
			}
			System.out.println("read done");
		} catch (Exception e) {
			e.printStackTrace();
		}finally {
			if(fis !=null) try{fis.close();}catch(Exception e) {}
			if(fos !=null) try{fos.close();}catch(Exception e) {}
		}
	}
```

### Keyboard IO

```java
	public static void main(String[] args)
    throws IOException {
		int read;
		FileOutputStream fos = null;
		try {
			fos = new 		FileOutputStream("res/keyboard1.txt");
			do {
				read = System.in.read();
				fos.write(read);
				if(read !='\n' && read!='\r') {
					System.out.println((char)read);	
				}
				
			}while(read !='x' && read != -1);
		} catch (Exception e) {
			e.printStackTrace();
		}finally {
			if(fos != null)
			try {fos.close();}catch(Exception e){}
		}
		
	}
	////////////////////////////////////////
	public static void main(String[] args) {
		FileWriter fw = null;
		InputStreamReader isr = null;
		BufferedReader br = null;
		try {
			isr = new InputStreamReader(System.in);
			br = new BufferedReader(isr);
			fw = new FileWriter("res/keyboard2.txt");
			String line;
			while((line = br.readLine())!=null) {
				System.out.println(line);
				fw.write(line);
				fw.write("\r\n");
			}
		} catch (Exception e) {
			e.printStackTrace();
		}finally {
			IOUtill.close(fw);
			IOUtill.close(br);
			IOUtill.close(isr);
		}
	}
```

