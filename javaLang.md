1. Map初始化构造器
  ```java
  HashMap<String, String > h = new HashMap<String, String>(){{
        put("a","b");    
  }}
  ```
2. //region
   //endregion
   
3. List初始化构造器
    ```
    Arrays.asList("Buenos Aires", "Córdoba", "La Plata");
    
    ArrayList<String> list = new ArrayList<String>() {{
        add("A");
        add("B");
        add("C");
    }}
    ```
4. 对象初始化构造器
    ```
    User user = new User(){ // 注意这里一共是两个花括号!!!
        {
            username = "大头"; // public的属性可以直接赋值 
            setPassword("654321"); // 私有的要通过setter赋值
        }
    }; 
    ```
