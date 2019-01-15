## Part Ⅱ Standard Library
C++ Primer 5th edition
### Cpt.11 关联容器
associative-container: 主要包含map和set两种

按关键字有序保存元素的 |说明  
:--:|:--:
map |关联数组
set |关键字即值，只保存关键字
multimap |key可重复出现，相同key**相邻**存储
multiset |同上
|
无序集合|说明
unordered_map|用哈希函数组织的map
unordered_set|同上
unordered_multimap|
unordered_multiset|  

#### 关联容器的使用
##### 概述
- 使用map： 
  - `map<string, size_t> word_count; string word; ++word_count[word];`
- 使用set
  - `set<string> exclude = {"the", "but", "and", "or"}; `
  - `if (exclude.find(word) == exclude.end()) ++word_count[word];`
##### 有序容器
- 比较关键字
  - 默认使用 < 来比较关键字的大小，可以自己定义，但操作须满足**严格弱序**（可看做小于等于）
  - 凡是定义了“行为正常”的<运算的类型均可作为有序容器的关键字
  - 比较类型可以通过函数指针来定义：
  - `bool compareISBN(const Sales_data &lhs, const Sales_data &rhs) { return lhs.isbn() < rhs.isbn();}`
  - `multiset<Sales_data, decltype(compareISBN) *> bookstore(compareISBN);//在<>中支出自定义操作的类型，对于函数指针其声明须加*，compareISBN为构造函数的参数。`
##### pair类型
- `pair<string, string> author{"James", "Joyce"};//初始化可省略`
- 成员为public类型，分别为first和second
- 基本操作：
  - 初始化：`pair<T1, T2> p = {v1, v2};` 等价于 `pair<T1, T2> p(v1, v2);`
  - p.first; p.second;
  - p1 relop p2;
  
##### 关联容器操作
- 在关联容器中额外有如下类型别名：
  - key_type
  - mapped_type 关键字关联的类型 `map<string, int>::mapped_type v5; //v5是一个int`
  - value_type 对于map而言其保存`pair<const key_type, mapped_type>`，对于set为key_type
- 使用迭代器访问
  - 返回一个value_type的引用，注意对于pair.first和set其迭代器均为const
- 插入元素
  - `set1.insert(vect1.begin(), vect1.end());`或`{}`
  - 返回一个pair，first为指向关键字元素的迭代器，second为bool型，失败（如已存在）则不执行插入并返回false
  - 向map中添加元素时须为pair类型
- 删除元素
  - `c.erase(key_type); `//从c中删除每个关键字为key_type的元素
  - 传递一个/两个迭代器元素，返回指向删除后的下一个元素的迭代器
- 在map中的下标操作：
  - `word_count["Anna"] = 1;`如果Anna不存在则**添加该关键字**并赋值为1，因此若map为const则不适用此方法
  - `c.at(k)`若k不在c中则抛出异常
  - 其返回值为mapped_type，因此可直接修改值的大小，但与迭代器返回的value_type并不相同
- 访问元素
  - 查找是否存在： find(v) //返回迭代器, count(v)//返回次数
  - `lower_bound(k)` `upper_bound(k)` `equal_range(k)/*返回一个迭代器pair，指向关键字符合k的元素的范围，不存在则均为c.end()`