### 1. 請用簡單的方式敘述以下每一行程式碼： ###
    a = 1 
    @a = 2
    @@a = 5
    user = User.new
    user.name
    user.name = "Joe"

### Answer： ###
- `a = 1`，是宣告一個變數a，並且將變數a的值設為1。
- `@a = 2`，是宣告一個實例變數a，並且將實例變數a的值設為2。
- `@@a = 5`，是宣告一個類別變數a，並且將類別變數a的值設為5。
- `user = User.new`，是建立一個User的類別實例，並將其值指派給變數user。
- `user.name`，其意義是取得user物件的實例變數name。
- `user.name = “Joe”`，其意義是將"Joe"字串指派給user物件的實例變數name。

### 2. 什麼是 module? 請寫一段程式碼說明一個 class 要如何使用一個 module 裡面的 method? ###
### Answer： ###
(1) module是將相關的方法與常數包在一起，提供特定的功能讓需要的人使用。就像是一個工具箱一樣。

- module的限制有：不可以new，無法被實例化；不能被繼承。
- module的功用有：定義一些公用的函式庫，提供他人使用，例如Ruby裡的Math模組
讓其他類別透過mixin方式引用，以擴充功能。

(2) 參考程式碼如下所示：

```ruby
    module Fly
      def fly
        puts "I can believe I can fly!"
      end
    end
    class People
      include Fly
        def initialize
      end
      def walk
        puts "keep walking!"
      end
    end
    people = People.new
    people.fly
```

### 3. 請說明 class variable 和 instance variable 之間的差別 ###
### Answer： ###
(1) class variable：

- 宣告方式：@@name，變數名稱前加上@@，並且在類別的最外層宣告。
- 使用方式：使用時直接透過類別名稱.變數名稱就可以使用。

(2) Instance variable：

- 宣告方式：@name，變數名稱前加上@，並且只能宣告在函式裡，通常是宣告在initialize。
- 使用方式：必須先建立好實例，才可以透過實例物件來進行存取

### 4. 請說明 class method 和 instance method 之間的差別 ###
### Answer： ###
(1) class method：

- 宣告方式：在method名稱前加上self.。
- 使用方式：使用時直接透過類別名稱.method名稱就可以使用。

(2) instance method：

- 宣告方式：一般method的宣告方式。
- 使用方式：必須先建立好實例，才可以透過實例物件來進行存取。

### 5. 如果今天我為一個叫 User 的 class 產生一個新物件的方式是: ###
    User.new("Bob", "male", "Engineer")
###    請寫出 User class 的 initialize method ###
### Answer： ###
此 User class 的 initialize method 程式碼，簡述如下：
```ruby
    class User
      def initialize(name, sex, job)
        @name = name
        @sex = sex
        @job = job
      end
    end
```

### 6. 在： A. 一個 class 裡，method 外面 B. 一個 class 裡，instance method 裡 self 分別是指向什麼? ###
### Answer： ###
- 在一個 class 裡，將 self 放在 method 外面，就等同於是在類別層級的宣告，此時的 Self 是指向 class。
- 如果在一個 class 時，將 self 放在 instance method 裡面，則是等同於物件層級的宣告，此時的 self 是指向呼叫該 method 的物件。

### 7. attr_accessor 的功能是什麼，它和 attr_reader、attr_writer 之間的差別是什麼？ ###
### Answer： ###
-  `attr_accessor` 會在 Ruby 的 class 裡產生一對 getter 以及 setter 的 method。
-  `attr_reader` 則只會產生 getter 的 method，而 `attr_writer` 只會產生 Setter 的 method。
- 在Ruby的類別裡宣告的實例變數，為了保持資訊隱藏的特性，Ruby的變數預設都是被保護的，也就是外部無法直接存取。如果真的要取得或是設定，則必須寫對應的函式才能達到。但是如果每個實例變數都要加上對應的存取函式，將會造成不方便。所以只要加上 `attr_accessor`、`attr_reader`、`attr_writer` 這些指令就可以直接存取。

### 8. 請說明 public 和 private method 之間的不同 ###
### Answer： ###
ruby中，method存取權限分為三種 public、private、protected，其中 public 與 private 的差異說明如下：

- public：就是任何屬於這個 class 的物件都能使用。也就是可以在程式的任何地方被使用。
- private：是只有在 class 內部才可以存取，適用於有些時候，你希望一些 method 不會被程式的其他地方使用到(像是金流、身分證字號 etc.)。
- 在應用上，盡量把預期會經常改變的程式碼寫成 private methods，不常改變/穩定的方法則寫成 public methods，避免修改 method 的時候，所有依靠該 method 的程式碼也要一起修改。

### 9. 請說明 Inheritance 和 Module 之間的差別，它們分別是用於哪些情況？ 請舉例說明 ###
### Answer： ###
- Inheritance (繼承)：當我們希望在建立新的 class 時，新的 class 也包含了舊的 class 的方法和特性，這時就可以使用 inheritance(繼承)，讓我們不用重新寫很多東西。
- Module (模組)：Ruby 使用 Module 來解決多重繼承的問題。不同類別但是要擁有相同的方法，就可以改放在 Module 裡面，然後 include 它即可。可把 module 想像成工具箱，它並不是 class，沒有實例、不可 new，只能被 include 到其他 class 裡面使用。
- class(類別)可以透過Inheritance(繼承)或引用Module(模組)的方式來擴充功能，達到程式碼再利用的特性。但是繼承耦合度過高，無法很有彈性地去擴充，有很多相似的功能卻要被重複撰寫幾次。如果透過Module(模組)，將各種相同的功能抽離出來，定義為一個Module(模組)，則可彈性地在需要的class(類別)裡去引用，來達到擴充與再利用的目的。
- 只能為一個 class 建立子類別，但卻可以 mix 很多 module。如果今天需要 "是某個..."("Is a")的關係，就用 inheritance(繼承)，如過需要的是 "擁有某項行為"("has a")的概念，則就用 module(模組)。
- 例如：蝙蝠是屬於一種哺乳動物，就可讓 Bat Inheritance(繼承) Mammal；而蝙蝠具有飛行的能力，但並非所有哺乳動物都會飛，所以可讓 Bat include 擁有 fly 這個 method 的 module。
 
### 10. 若今天有一個 class 有 include 一個 module，他的 parent class 和 sub class 是否可以使用該 module 裡的 method? ###
### Answer： ###
- 他的sub class則可以使用該 module 裡的 method。
- 但他的parent class無法使用 module 裡的 method。

### 11. 請間單說明什麼是 Relational Database，什麼是 SQL ###
### Answer： ###
- Relational Badabase(關聯式資料庫)是將資料建立一組關係模型，再依此基礎建出系統架構的資料庫。資料依照一定的結構，存放在資料庫管理系統建立的檔案中，稱為資料庫; 資料庫由資料表構成，每張資料表則由許多筆記錄所組成，每筆記錄又以許多欄位組合而成，每個欄位則存放著一筆資料。在關聯式資料庫中，將每個資料表視為一個實體，每個實體則有屬性描述之，而這些屬性就稱為鍵值。資料表內用來識別記錄及提供索引的鍵值，稱為主鍵；不同於主鍵，但也具備資料索引功能的稱為次要鍵；以及資料表中，引用其它表單內資料的外來鍵等。對於關聯式資料庫中的資料表，用戶可以透過新增、刪除和修改等指令來異動資料表中的資料，而不會影響資料表中的其他資料。
- SQL來自Structural Query Language(結構化查詢語言)，是一種特殊目的的程式語言，一般用於資料庫中的標準資料查詢語法，所以SQL可視為應用程式與資料庫之間溝通的語言，是目前關聯式資料庫管理系統的標準語言。