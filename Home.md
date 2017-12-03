Welcome to the Hibernate-Configuation-file wiki!

* Product.java (My POJO class)
* Product.hbm.xml  (Xml mapping file )
* hibernate.cfg.xml  (Xml configuration file)
* ClientForSave.java (java file to write our hibernate logic)


--->product.java


public class Product {
	private int productId;
	private String proName;
	private double price;
	public int getProductId() {
		return productId;
	}
	public void setProductId(int productId) {
		this.productId = productId;
	}
	public String getProName() {
		return proName;
	}
	public void setProName(String proName) {
		this.proName = proName;
	}
	public double getPrice() {
		return price;
	}
	public void setPrice(double price) {
		this.price = price;
	}

}


----->product.hbm.xml

<?xml version="1.0"?>
<!DOCTYPE hibernate-mapping PUBLIC
"-//Hibernate/Hibernate Mapping DTD 3.0//EN"
"http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
 
<hibernate-mapping>
<class name="Product" table="PRODUCTS">
 
<id name="productId" column="pid"  >
<generator class="assigned" />
</id>
 
<property name="proName" column="pname" />
<property name="price"/>
 
</class>
</hibernate-mapping>

------>hibernate.cfg.xml

<?xml version='1.0' encoding='UTF-8'?>
<hibernate-configuration>
<session-factory>
 
<!-- Related to the connection START -->
<property name="connection.driver_class">com.mysql.jdbc.Driver
</property>
<property name="connection.url">jdbc:mysql://localhost:3306/jpadb</property>
<property name="connection.user">root</property>
<property name="connection.password">sandy</property>
<!-- Related to the connection END -->
 
<!-- Related to hibernate properties START -->
<property name="show_sql">true </property>
<property name="dialet">org.hibernate.dialect.OracleDialect </property>
<property name="hbm2ddl.auto">update </property>
<!-- Related to hibernate properties END -->
 
<!-- Related to mapping START -->
<mapping resource="product.hbm.xml" />
<!-- Related to the mapping END -->
 
</session-factory>

----->Client.java

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;
 
public class ClientForSave { 
 
 public static void main(String[] args)
 {
 
 Configuration cfg = new Configuration();
 cfg.configure("hibernate.cfg.xml"); 
 
 SessionFactory factory = cfg.buildSessionFactory();
 Session session = factory.openSession();
 Product p=new Product();
 
 p.setProductId(101);
 p.setProName("iPhone");
 p.setPrice(25000);
 
 Transaction tx = session.beginTransaction();
 session.save(p);
 System.out.println("Object saved successfully.....!!");
 tx.commit();
 session.close();
 factory.close();
 }
 
}

