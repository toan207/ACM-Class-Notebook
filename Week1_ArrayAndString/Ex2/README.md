# Bài 2
* **Đề bài:** Cho một chuỗi gồm các kí tự từ a đến z. Một chuỗi được gọi là Alpha nếu mỗi kí tự chỉ xuất hiện 1 lần trong chuỗi. Kiểm tra xem 1 dãy có phải là Alpha hay không nếu có in ra YES , nếu không in ra NO.
* >Đầu vào là 1 chuỗi kí tự có độ dài tối đa 10^6 phần tử.*

* **Vd1:**
    * **INPUT:**    abcder  
    * **OUTPUT:**   YES  
* **Vd2:**
    * **INPUT:**    degef  
    * **OUTPUT:**   NO  

* **Ý tưởng:**  
  * Đếm sự xuất hiện của từng kí tự xem kí tự nào xuất hiện 2 lần thì dùng chương trình và in ra NO, nếu chạy đến cuối chuỗi mà chưa có kí tự nào xuất hiện 2 lần thì in ra YES.
  * Vì tổng số kí tự trên bảng chữ cái là mà mỗi kí tự chỉ được xuất hiện 1 lần nên chuỗi nào có độ dài lơn hơn số lượng kí tự thì có thể in ra NO ngay lập tức.
  * Giải theo cách chuyển kí tự về số rồi sắp xếp chuỗi theo chiều tăng hoặc giảm dần. Kiểm tra từ đầu đên cuối chuỗi nêú 2 kí tự cạnh nhau giống nhau thì in ra NO và dừng chương trình. Nếu không in ra YES.
  * Nhập luôn số lần xuất hiện của kí tự vào mảng có Index là các kí tự. Kí tự nào xuất hiện 2 lần thì in ra NO. Nếu không in ra YES.
* **Code:**
  * **C++**
    ```
    #include <bits/stdc++.h>
    #define pb push_back
    using namespace std;
    int main(){
        string s;
        cin>>s;
        int ch;
        vector <int> v;
        if (s.length()>26){
            cout<<"NO"<<endl;
            return 0;
        }
        for(int i=0;i<s.length();i++){
            ch=s[i];
            v.pb(ch);
        }
        sort(v.begin(), v.end());
        int i=1;
        while (i<s.size()){
            if(v[i-1]==v[i]){
                cout<<"NO"<<endl;
                return 0;
            }
            i++;
        }
        cout<<"YES"<<endl;
        return 0;
    }
    ```
  * **Python**
    ```
    s = input()

    if len(s) > 26:
        print('NO')
    else:
        alphabet = [0] * (ord('z') - ord('a') + 1)

        for i in s:
            alphabet[ord(i) - ord('a')] += 1
            if alphabet[ord(i) - ord('a')] > 1:
                print('NO')
                exit()

        print('YES')
    ```