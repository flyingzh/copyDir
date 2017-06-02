# 拷贝文件夹到指定文件夹

   /**
	 * 拷贝文件夹到一个新的文件
	 * 
	 * @param newPath 要拷贝的文件路径
	 * @param oldPath 要拷贝到哪个路径
	 * @throws IOException 异常抛出由调用者处理
	 */
   
	public static void copyDirs(String oldPath, String newPath) throws IOException {
		(new File(newPath)).mkdirs();
		File f = new File(oldPath);
		String[] list = f.list();
		File temp = null;
		for (String file : list) {
			temp = new File(oldPath + "\\" + file);
			if (temp.isFile()) {
				BufferedInputStream inputStream = new BufferedInputStream(new FileInputStream(temp));
				BufferedOutputStream outputStream = new BufferedOutputStream(new FileOutputStream(newPath + "\\" + temp.getName()));
				int len;
				byte[] bs = new byte[1024 * 4];
				while ((len = inputStream.read(bs)) != -1) {
					outputStream.write(bs, 0, len);
				}
				outputStream.flush();
				outputStream.close();
				inputStream.close();
			}
			if (temp.isDirectory()) {
				copyDirs(oldPath + "\\" + file, newPath+"\\"+file);
			}
		}
	}
