###1、安装mybatis插件,找到mybatis_plus.jar包的位置,在C:\Users\LZHL\.IntelliJIdea2016.3\config\plugins\mybatis_plus\lib

###2、新建一个Java Project,把mybatis_plus.jar和javassist-3.17.1.jar添加到工程的Libary

###3、新建一个Class:
```java

package javaassist;

import javassist.CannotCompileException;
import javassist.ClassPool;
import javassist.CtClass;
import javassist.CtMethod;

import java.io.IOException;

/**
* @Author LZHL
* @Create 2017-02-17 15:19
* @Description
*/
public class Main {
　　public static void main(String[] args)throws Exception{
　　　　ClassPool pool = ClassPool.getDefault();
　　　　CtClass driverClass = pool.get("com.seventh7.mybatis.ref.license.ActivationDriver");
　　　　CtClass javaUtil = pool.get("com.seventh7.mybatis.util.JavaUtils");
　　　　CtMethod activate = driverClass.getMethod("activate","(Ljava/lang/String;)Lcom/seventh7/mybatis/ref/license/ActivationResult;");
　　　　CtMethod refValid = javaUtil.getDeclaredMethod("refValid");
　　　　try{
　　　　　　refValid.setBody("{return true;}");
　　　　} catch(CannotCompileException e) {
　　　　　　e.printStackTrace();
　　　　}
　　　　System.out.println(activate);
　　　　try{
　　　　　　activate.setBody("{com.seventh7.mybatis.ref.license.LicenseData licenseData = new com.seventh7.mybatis.ref.license.LicenseData(\"1\", \"2\");com.seventh7.mybatis.ref.license.ActivationResult res =com.seventh7.mybatis.ref.license.ActivationResult.success(licenseData); return res;}");
　　　　} catch(CannotCompileException e) {
　　　　　　e.printStackTrace();
　　　　}
　　　　try{
　　　　　　driverClass.writeFile("activate");
　　　　　　javaUtil.writeFile("activate");
　　　　} catch(CannotCompileException e) {
　　　　　　e.printStackTrace();
　　　　} catch(IOException e) {
　　　　　　e.printStackTrace();
　　　　}
　　}
}

```
####执行main方法会在当前项目下生成一个activate文件夹，将activate文件夹下的com文件夹拷到mybatis_plus.jar所在目录下，在当前目录打开CMD窗口
执行jar uvf mybatis_plus.jar com(**注意：执行命令前先退出Idea**)
到些破解完成，重启Idea即可生效.
