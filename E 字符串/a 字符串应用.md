==getline(cin,s)==会获取前一个输入的换行符，可以在前面利用cin.ignore()消去
```cpp
string s,s1;
char s2[100],s3[100];
void solve(){
   cin>>s>>s1;
转换大小写
transform(s.begin(),s.end(),s.begin(),::toupper);//=s.begin()+3//第三个参数是存放的位置
s[2]=toupper(s[2]);//tolower(s[i]);
int t=s.find(s[2],t);//找不到返回-1//可查找子字符串及开始的位置
//不知道返回什么的时候auto真的很好用//前面有s.了，括号里就直接用下标位置序号就行
//字符串截取
(auto t=)//s1=s.substr(begin,lenght);
//替换
s.replace(begin,length,"str");
//排序
sort(s.begin(), s.end());
//删除、清除、增加
s.erase(begin,length);
s.clear();s.push_back();
//插入
s.insert(begin,"str")
//拼接
s.append(s1);
//c中的strcat(s2,s.c_str()+3);
  cout<<s<<endl;
  return ;
}
```