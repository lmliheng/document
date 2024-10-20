### 项目
[来源](https://how2j.cn/k/hutubill/hutubill-backup/754.html#nowhere)

### 目录
```bash
├───src/
│   ├───HutuMainFrame.java
│   ├───dao/
│   │   ├───CategoryDAO.java
│   │   ├───ConfigDAO.java
│   │   ├───RecordDAO.java
│   ├───entity/
│   │   ├───Category.java
│   │   ├───Config.java
│   │   ├───Record.java
│   ├───gui/
│   │   ├───frame/
│   │   │   ├───MainFrame.java
│   │   ├───listener/
│   │   │   ├───BackupListener.java
│   │   │   ├───CategoryListener.java
│   │   │   ├───ConfigListener.java
│   │   │   ├───RecordListener.java
│   │   │   ├───RecoverListener.java
│   │   │   ├───ToolBarListener.java
│   │   ├───model/
│   │   │   ├───CategoryComboBoxModel.java
│   │   │   ├───CategoryTableModel.java
│   │   ├───page/
│   │   │   ├───SpendPage.java
│   │   ├───panel/
│   │   │   ├───BackupPanel.java
│   │   │   ├───CategoryPanel.java
│   │   │   ├───ConfigPanel.java
│   │   │   ├───MainPanel.java
│   │   │   ├───RecordPanel.java
│   │   │   ├───RecoverPanel.java
│   │   │   ├───ReportPanel.java
│   │   │   ├───SpendPanel.java
│   │   │   ├───WorkingPanel.java
│   ├───service/
│   │   ├───CategoryService.java
│   │   ├───ConfigService.java
│   │   ├───RecordService.java
│   │   ├───ReportService.java
│   │   ├───SpendService.java
│   ├───startup/
│   │   ├───Bootstrap.java
│   ├───test/
│   │   ├───Test.java
│   ├───util/
│   │   ├───CenterPanel.java
│   │   ├───ChartUtil.java
│   │   ├───CircleProgressBar.java
│   │   ├───ColorUtil.java
│   │   ├───DateUtil.java
│   │   ├───DBUtil.java
│   │   ├───GUIUtil.java
│   │   ├───MysqlUtil.java
```
### DAO

#### CategoryDAO
```java
package dao;
 
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;
 
import entity.Category;
import util.DBUtil;
 
public class CategoryDAO {
 
    public int getTotal() {
        int total = 0;
        try (Connection c = DBUtil.getConnection(); Statement s = c.createStatement();) {
 
            String sql = "select count(*) from category";
 
            ResultSet rs = s.executeQuery(sql);
            while (rs.next()) {
                total = rs.getInt(1);
            }
 
            System.out.println("total:" + total);
 
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
        return total;
    }
 
    public void add(Category category) {
 
        String sql = "insert into category values(null,?)";
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
 
            ps.setString(1, category.name);
 
            ps.execute();
 
            ResultSet rs = ps.getGeneratedKeys();
            if (rs.next()) {
                int id = rs.getInt(1);
                category.id = id;
            }
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
    }
 
    public void update(Category category) {
 
        String sql = "update category set name= ? where id = ?";
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
 
            ps.setString(1, category.name);
            ps.setInt(2, category.id);
 
            ps.execute();
 
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
 
    }
 
    public void delete(int id) {
 
        try (Connection c = DBUtil.getConnection(); Statement s = c.createStatement();) {
 
            String sql = "delete from category where id = " + id;
 
            s.execute(sql);
 
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
    }
 
    public Category get(int id) {
        Category category = null;
 
        try (Connection c = DBUtil.getConnection(); Statement s = c.createStatement();) {
 
            String sql = "select * from category where id = " + id;
 
            ResultSet rs = s.executeQuery(sql);
 
            if (rs.next()) {
                category = new Category();
                String name = rs.getString(2);
                category.name = name;
                category.id = id;
            }
 
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
        return category;
    }
 
    public List<Category> list() {
        return list(0, Short.MAX_VALUE);
    }
 
    public List<Category> list(int start, int count) {
        List<Category> categorys = new ArrayList<Category>();
 
        String sql = "select * from category order by id desc limit ?,? ";
 
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
 
            ps.setInt(1, start);
            ps.setInt(2, count);
 
            ResultSet rs = ps.executeQuery();
 
            while (rs.next()) {
                Category category = new Category();
                int id = rs.getInt(1);
                String name = rs.getString(2);
                category.id = id;
                category.name = name;
                categorys.add(category);
            }
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
        return categorys;
    }
 
}
```
#### ConfigDAO.java
```java
package dao;
 
import java.sql.Connection;
 
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;
 
import entity.Config;
import util.DBUtil;
 
public class ConfigDAO {
 
    public int getTotal() {
        int total = 0;
        try (Connection c = DBUtil.getConnection(); Statement s = c.createStatement();) {
 
            String sql = "select count(*) from config";
 
            ResultSet rs = s.executeQuery(sql);
            while (rs.next()) {
                total = rs.getInt(1);
            }
 
            System.out.println("total:" + total);
 
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
        return total;
    }
 
    public void add(Config config) {
 
        String sql = "insert into config values(null,?,?)";
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
            ps.setString(1, config.key);
            ps.setString(2, config.value);
            ps.execute();
            ResultSet rs = ps.getGeneratedKeys();
            if (rs.next()) {
                int id = rs.getInt(1);
                config.id = id;
            }
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
    }
 
    public void update(Config config) {
 
        String sql = "update config set key_= ?, value=? where id = ?";
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
 
            ps.setString(1, config.key);
            ps.setString(2, config.value);
            ps.setInt(3, config.id);
 
            ps.execute();
 
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
 
    }
 
    public void delete(int id) {
 
        try (Connection c = DBUtil.getConnection(); Statement s = c.createStatement();) {
 
            String sql = "delete from config where id = " + id;
 
            s.execute(sql);
 
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
    }
 
    public Config get(int id) {
        Config config = null;
 
        try (Connection c = DBUtil.getConnection(); Statement s = c.createStatement();) {
 
            String sql = "select * from config where id = " + id;
 
            ResultSet rs = s.executeQuery(sql);
 
            if (rs.next()) {
                config = new Config();
                String key = rs.getString("key_");
                String value = rs.getString("value");
                config.key = key;
                config.value = value;
                config.id = id;
            }
 
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
        return config;
    }
 
    public List<Config> list() {
        return list(0, Short.MAX_VALUE);
    }
 
    public List<Config> list(int start, int count) {
        List<Config> configs = new ArrayList<Config>();
 
        String sql = "select * from config order by id desc limit ?,? ";
 
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
 
            ps.setInt(1, start);
            ps.setInt(2, count);
 
            ResultSet rs = ps.executeQuery();
 
            while (rs.next()) {
                Config config = new Config();
                int id = rs.getInt(1);
                String key = rs.getString("key_");
                String value = rs.getString("value");
                config.id = id;
                config.key = key;
                config.value = value;
                configs.add(config);
            }
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
        return configs;
    }
 
    public Config getByKey(String key) {
        Config config = null;
        String sql = "select * from config where key_ = ?" ;
        try (Connection c = DBUtil.getConnection(); 
                PreparedStatement ps = c.prepareStatement(sql);
            ) {
             
            ps.setString(1, key);
            ResultSet rs =ps.executeQuery();
 
            if (rs.next()) {
                config = new Config();
                int id = rs.getInt("id");
                String value = rs.getString("value");
                config.key = key;
                config.value = value;
                config.id = id;
            }
 
        } catch (SQLException e) {
 
            e.printStackTrace();
        }
        return config;
    }
 
}
```

#### RecordDAO

```java
package dao;
 
import java.sql.Connection;
 
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;
 
import entity.Record;
import util.DBUtil;
import util.DateUtil;
  
public class RecordDAO {
  
    public int getTotal() {
        int total = 0;
        try (Connection c = DBUtil.getConnection(); Statement s = c.createStatement();) {
  
            String sql = "select count(*) from record";
  
            ResultSet rs = s.executeQuery(sql);
            while (rs.next()) {
                total = rs.getInt(1);
            }
  
            System.out.println("total:" + total);
  
        } catch (SQLException e) {
  
            e.printStackTrace();
        }
        return total;
    }
  
    public void add(Record record) {
  
        String sql = "insert into record values(null,?,?,?,?)";
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
            ps.setInt(1, record.spend);
            ps.setInt(2, record.cid);
            ps.setString(3, record.comment);
            ps.setDate(4, DateUtil.util2sql(record.date));
  
            ps.execute();
  
            ResultSet rs = ps.getGeneratedKeys();
            if (rs.next()) {
                int id = rs.getInt(1);
                record.id = id;
            }
        } catch (SQLException e) {
  
            e.printStackTrace();
        }
    }
  
    public void update(Record record) {
  
        String sql = "update record set spend= ?, cid= ?, comment =?, date = ? where id = ?";
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
  
              ps.setInt(1, record.spend);
              ps.setInt(2, record.cid);
              ps.setString(3, record.comment);
              ps.setDate(4, DateUtil.util2sql(record.date));
              ps.setInt(5, record.id);
  
            ps.execute();
  
        } catch (SQLException e) {
  
            e.printStackTrace();
        }
  
    }
  
    public void delete(int id) {
  
        try (Connection c = DBUtil.getConnection(); Statement s = c.createStatement();) {
  
            String sql = "delete from record where id = " + id;
  
            s.execute(sql);
  
        } catch (SQLException e) {
  
            e.printStackTrace();
        }
    }
  
    public Record get(int id) {
        Record record = null;
  
        try (Connection c = DBUtil.getConnection(); Statement s = c.createStatement();) {
  
            String sql = "select * from record where id = " + id;
  
            ResultSet rs = s.executeQuery(sql);
  
            if (rs.next()) {
                record = new Record();
                int spend = rs.getInt("spend");
                int cid = rs.getInt("cid");
                String comment = rs.getString("comment");
                Date date = rs.getDate("date");
                 
                record.spend=spend;
                record.cid=cid;
                record.comment=comment;
                record.date=date;
                record.id = id;
            }
  
        } catch (SQLException e) {
  
            e.printStackTrace();
        }
        return record;
    }
  
    public List<Record> list() {
        return list(0, Short.MAX_VALUE);
    }
     
    public List<Record> list(int start, int count) {
        List<Record> records = new ArrayList<Record>();
  
        String sql = "select * from record order by id desc limit ?,? ";
  
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
  
            ps.setInt(1, start);
            ps.setInt(2, count);
  
            ResultSet rs = ps.executeQuery();
  
            while (rs.next()) {
                Record record = new Record();
                int id = rs.getInt("id");
                int spend = rs.getInt("spend");
                int cid = rs.getInt("cid");
                 
                 String comment = rs.getString("comment");
                 Date date = rs.getDate("date");
                  
                 record.spend=spend;
                 record.cid=cid;
                 record.comment=comment;
                 record.date=date;
                 record.id = id;
                records.add(record);
            }
        } catch (SQLException e) {
  
            e.printStackTrace();
        }
        return records;
    }
     
    public List<Record> list(int cid) {
        List<Record> records = new ArrayList<Record>();
  
        String sql = "select * from record where cid = ?";
  
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
  
            ps.setInt(1, cid);
  
            ResultSet rs = ps.executeQuery();
  
            while (rs.next()) {
                Record record = new Record();
                int id = rs.getInt("id");
                int spend = rs.getInt("spend");
                 
                 String comment = rs.getString("comment");
                 Date date = rs.getDate("date");
                  
                 record.spend=spend;
                 record.cid=cid;
                 record.comment=comment;
                 record.date=date;
                 record.id = id;
                records.add(record);
            }
        } catch (SQLException e) {
  
            e.printStackTrace();
        }
        return records;
    }    
     
    public List<Record> listToday(){
        return list(DateUtil.today());
    }
     
    public List<Record> list(Date day) {
        List<Record> records = new ArrayList<Record>();
        String sql = "select * from record where date =?";
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
            ps.setDate(1, DateUtil.util2sql(day));
 
            ResultSet rs = ps.executeQuery();
            while (rs.next()) {
                Record record = new Record();
                int id = rs.getInt("id");
                int cid = rs.getInt("cid");
                int spend = rs.getInt("spend");
                 
                 String comment = rs.getString("comment");
                 Date date = rs.getDate("date");
                  
                 record.spend=spend;
                 record.cid=cid;
                 record.comment=comment;
                 record.date=date;
                 record.id = id;
                 records.add(record);
            }
        } catch (SQLException e) {
  
            e.printStackTrace();
        }
        return records;
    }            
     
    public List<Record> listThisMonth(){
        return list(DateUtil.monthBegin(),DateUtil.monthEnd());
    }
     
    public List<Record> list(Date start, Date end) {
        List<Record> records = new ArrayList<Record>();
        String sql = "select * from record where date >=? and date <= ?";
        try (Connection c = DBUtil.getConnection(); PreparedStatement ps = c.prepareStatement(sql);) {
            ps.setDate(1, DateUtil.util2sql(start));
            ps.setDate(2, DateUtil.util2sql(end));
            ResultSet rs = ps.executeQuery();
            while (rs.next()) {
                Record record = new Record();
                int id = rs.getInt("id");
                int cid = rs.getInt("cid");
                int spend = rs.getInt("spend");
                 
                 String comment = rs.getString("comment");
                 Date date = rs.getDate("date");
                  
                 record.spend=spend;
                 record.cid=cid;
                 record.comment=comment;
                 record.date=date;
                 record.id = id;
                 records.add(record);
            }
        } catch (SQLException e) {
  
            e.printStackTrace();
        }
        return records;
    }        
  
}
```

### entity
#### Category
```java
package entity;
 
public class Category {
    public int id;
    public String name;
     
    public int recordNumber;
     
    public int getRecordNumber() {
        return recordNumber;
    }
    public void setRecordNumber(int recordNumber) {
        this.recordNumber = recordNumber;
    }
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
     
    public String toString(){
        return name;
    }
}
```
#### Config
```java
package entity;
 
public class Config {
 
    public int id;
    public String key;
    public String value;
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    public String getKey() {
        return key;
    }
    public void setKey(String key) {
        this.key = key;
    }
    public String getValue() {
        return value;
    }
    public void setValue(String value) {
        this.value = value;
    }
     
}
```
#### Record
```java
package entity;
 
import java.util.Date;
 
public class Record {
    public int spend;
    public int id;
    public int cid;
    public String comment;
    public Date date;
     
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    public int getCid() {
        return cid;
    }
    public void setCid(int cid) {
        this.cid = cid;
    }
    public String getComment() {
        return comment;
    }
    public void setComment(String comment) {
        this.comment = comment;
    }
    public Date getDate() {
        return date;
    }
    public void setDate(Date date) {
        this.date = date;
    }
    public int getSpend() {
        return spend;
    }
    public void setSpend(int spend) {
        this.spend = spend;
    }
 
}
```

