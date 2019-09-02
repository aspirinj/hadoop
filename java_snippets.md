
#### DataOutputStream & DataInputStream
```java
DataOutputStream dos = new DataOutputStream(new FileOutputStream("/home/howard/Downloads/a.txt"));
		dos.writeInt(8);
		dos.writeUTF("你好啊");
		dos.close();
		
		DataInputStream dis = new DataInputStream(new FileInputStream("/home/howard/Downloads/a.txt"));
		System.out.println(dis.readInt());
		System.out.println(dis.readUTF());
		dis.close();
		
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNDg1MDM1NTUsMTc0NTg2MTQ3MywtMT
Q5NDEwNjE5OF19
-->