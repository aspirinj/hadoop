
#### DataOutputStream & DataInputStream
```java
DataOutputStream dos = new DataOutputStream(new FileOutputStream("a.txt"));
	dos.writeInt(8);
	dos.writeUTF("你好啊");
	dos.close();
		
DataInputStream dis = new DataInputStream(new FileInputStream("a.txt"));
	System.out.println(dis.readInt());
	System.out.println(dis.readUTF());
	dis.close();
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4ODkzMDU4MzMsMTc0NTg2MTQ3MywtMT
Q5NDEwNjE5OF19
-->