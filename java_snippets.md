
#### DataOutputStream 
```java
DataOutputStream dos = new DataOutputStream(new FileOutputStream("/a.txt"));
	dos.writeInt(8);
	dos.close();
	dos.write("你好啊".getBytes("utf-8"));
	dos.writeUTF("你好啊");
		
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc0NTg2MTQ3MywtMTQ5NDEwNjE5OF19
-->