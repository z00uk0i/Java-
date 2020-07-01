Java常用代码
==

JavaSE
--
# 异常






SSM+Redis
--
# 反射
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class Reflect_zk {
	
	public void sayHello(String name) {
		System.out.println("Hello"+name);
	}
	
	//1.定义反射生成无参对象的方法s
	public Reflect_zk getInstance() {
		Reflect_zk object = null;
		try {
			object = (Reflect_zk) Class.forName("com.lean.ssm.chapter2.reflect.Reflect_zk")
					.newInstance();
		} catch (ClassNotFoundException | InstantiationException | IllegalAccessException ex) {
			ex.printStackTrace();
		}
		return object;
	}
	
	//2.定义反射生成实参为“张三”的对象的方法
	public Reflect_zk getInstance_Parameter() {
		Reflect_zk object = null;
	    try {
	        object = 
	            (Reflect_zk) 
	            Class.forName("com.lean.ssm.chapter2.reflect.Reflect_zk").
	            getConstructor(String.class).newInstance("张三");
	    } catch (ClassNotFoundException | InstantiationException 
	                | IllegalAccessException | NoSuchMethodException 
	                | SecurityException | IllegalArgumentException 
	                | InvocationTargetException ex) {
	            ex.printStackTrace();
	    }
	    return object;
	}
	
	//3.定义反射调用sayHello()的方法
	public Object reflectMethod() {
		Object returnObj = null;
		Reflect_zk target = new Reflect_zk();
		try {
			Method method = Reflect_zk.class.getMethod("sayHello", String.class);
			returnObj = method.invoke(target, "张三");
		} catch (NoSuchMethodException | SecurityException | IllegalAccessException | IllegalArgumentException
				| InvocationTargetException ex) {
			ex.printStackTrace();
		}
		return returnObj;
	}
	
	//4.将1和3结合到一起
	public Object reflect() {
		Reflect_zk object = null;
		try {
			object = (Reflect_zk) Class.forName("com.lean.ssm.chapter2.reflect.Reflect_zk")
					.newInstance();
			Method method = object.getClass().getMethod("sayHello", String.class);
			method.invoke(object, "张三");
		} catch (NoSuchMethodException | SecurityException | ClassNotFoundException | IllegalAccessException
				| IllegalArgumentException | InvocationTargetException | InstantiationException ex) {
			ex.printStackTrace();
		}
		return object;
	}
}

# Java设计模式
