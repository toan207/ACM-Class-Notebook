# Bài 1
* **Đề bài:** Cho 1 tấm vé số có 7 chữ số. Tấm vé số có dạng ABCDEG. Tấm vé được gọi là may mắn nếu tổng 3 chữ số đầu bằng tổng 3 chữ số cuối. Tính xác xuất để mua được 1 tấm vé may mắn.

* Vd các vé số may mắn là:
    * 0000000  
    * 2459137  

* **CÁCH 1:** Dùng 2 vòng for O(1000^2) 
  * **Ý tưởng:** 
      * Vì số tự nhiên có 7 chữ số nên 3 chữ số đầu và 3 chữ số cuối luôn là 999. Vậy nên ta sẽ tính 2 vòng lặp để tính tổng của từng cái này rồi đem so sánh với thằng còn lại. 
      * >Cách tính tổng 3 số bất kỳ VD: 123 = 1 + 2 + 3 = 6;
  * **Code:**
    * **JavaScript**  
        ```
        function calculatorNum(n) {
        var sum1 = 0;
        while( n != 0) {
            sum1 += n % 10;
            n = parseInt(n / 10);
        }
        return sum1;
        }
        function test1()  { 
        let sum1,sum2,temp=0;
        for(let i = 0 ; i < 999 ; i ++)  {
            sum1 = calculatorNum(i);
            for(let j = 0 ; j < 999 ; j ++) {
                sum2 = (calculatorNum(j));
                if(sum1 == sum2) {
                temp ++;
                }
            }
        }
        // temp ở đây là biến tính cái biến cố như mình nói ở trên 
        // Hàm Math.pow(a,b) => được hiểu là a ^ b;
        //console.log(temp)
        return temp / (Math.pow(10,6))
        }
        ```
* **CÁCH 2:** Sử dụng kĩ thuật đếm phân phối O(1000)
  * **Ý tưởng:** 
    * Vì 3 số chạy 000 => 999 vậy max 3 số là 27.
    * Vì tổng của 3 chữ số chỉ giao động trong khoảng từ 0 đến 27. Vì vậy ta tìm với mỗi trường hợp tổng của 3 số thì có bao nhiêu bộ 3 chữ số bằng với tổng đó( tạm gọi là n). Với mỗi cách trọn 3 chữ số đứng đầu ta có n cách chọn 3 chữ số đứng cuối nên ta có tổng bằng: n0^2 + n1^2+...+n27^2.
    * Ta đã chọn được 3 chữ số đầu và và 3 chữ số cuối nên để có tổng sô vé ta chỉ cần nhân với 10 là số hoán vị của chữ số thứ 4.
* **Code:**
  * **Javacript**
    ```
    function test2 () {
    // tạo  array có 27 phần tử;
    let temp = 0;
    let arr = new Array(27);
    for(let i = 0 ; i< 27 ; i ++) {
        // set up element for =0;
        arr[i]  = 0;

    }
    for(let i = 0  ; i < 999 ; i ++) {
        let sum =calculatorNum(i)
        arr[sum] ++ ;
    }
    for(let i = 0 ; i < 27 ; i ++) {
        //(2)
        temp += Math.pow(arr[i],2) ;
    }
    return temp / (Math.pow(10,6))
    }
    ```
  * **C++**
    ```
    #include <bits/stdc++.h>
    #define M 1000000
    using namespace std ;

    int calsum(int N ) {
    int sum = 0 , m ;
    while( N > 0)  {  
        m = N % 10 ;   
        sum = sum + m ;  
        N = N / 10 ;  
    }

    return sum ;
    }

    int main() {
    int A[28] ;
    double ans = 0.0 ;
    for(int i = 0 ; i < 28 ; i++)
        A[i] = 0 ;

    for(int i = 0 ; i <= 999 ; i++){
        int sum = calsum(i) ;
        A[sum]++;
    } 
    
    for(int i = 0 ; i < 28 ; i++)
        ans +=(double) (A[i] * A[i]) / M ;
    
    
    cout << ans ;
    return 0 ;  
    }
    ```
  * **Python**
    ```
    count = [0] * 28 # Tạo mảng 28 phần tử 0 đại diện cho 28 tổng của 3 chữ số 0 đến 27

    for i in range(1000): # Chạy vòng lặp đếm tổng số lượng xuất hiện của các tổng số có 3 chữ số tính từ 000
        mark = str(i)
        temp = 0

        for j in mark: # Tính tổng của 3 chữ số
            temp += int(j)

        count[temp] += 1

    sumLuckyTicket = 0

    for i in count: # Đếm các tấm vé may mắn
        sumLuckyTicket += i * i * 10

    ans = (sumLuckyTicket / int(1e6)) * 100
    ```

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
# Bài 3
* **Đề bài:** Cho 1 dãy các số nguyên. Sắp xếp lại dãy sao cho tất cả chữ số chẵn đứng bên trái tất cả các chữ số lẻ.

* **Vd1:**
    * **INPUT:**   
                5
                1 2 3 4 5

    * **OUTPUT:**   2 4 5 3 1
* **Vd2:**
    * **INPUT:**    
                5
                1 4 8 9 9

    * **OUTPUT:**   4 8 1 9 9

* **Ý tưởng:** 
  * **Cách 1:**
    Nhập vào các phần tử, dùng 2 biến để lưu Index đầu và cuối. Kiểm tra số nhập vào nếu là số chẵn thì lưu vào mảng tại Index đầu rồi tăng Index lên 1 đơn vị, nếu là số lẻ thì lưu vào mảng tại Index cuối rồi giảm Index đi 1 đơn vị.
  * **Code:**
    * **C++**
        ```
        #include <bits/stdc++.h>
        using namespace std;
        int main(){
            int n,m,h=0,k;
            cin>>n;
            k=n-1;
            int a[1000000];
            for(int i=0;i<n;i++){
                cin>>m;
                if(m%2==0) {
                    a[h]=m;
                    h++;
                }
                else {
                    a[k]=m;
                    k--;
                }
            }
            for(int i=0;i<n;i++) cout<<a[i]<<" ";
            return 0;
        }
        ```
  * **Cách 2:** 
    Tạo 1 biến mark = 0 để lưu giá trị lẻ đầu tiên trong mảng , dùng vòng lặp for để kiểm tra phần tử mang giá trị chẵn trong mảng , nếu chẵn thì ta đổi chỗ phần tử đó với phần tử ở vị trí mark rồi sau đó tăng biến mark thêm 1.
  * **Code:**
    * **JavaScript**
        ```
        function test5(arr) {
        let mark = 0;
        let temp;
        for(let i = 0 ; i < arr.length ; i++) {
            if(arr[i] % 2 == 0) {
            // đổi chỗ arr[mark] vs arr[i]
            temp = arr[mark];
            arr[mark] = arr[i];
            arr[i] = temp;
            mark ++;
            }
        }
        // Chạy thử tay nha 
        // mark = 0;
        // temp;
        // arr[0]= 1;
        // 0: mark = 0; arr = [1,2,3,4 ];
        // 1: temp =  arr[mark] = arr[0] = 1;
        // 1.1: arr[mark] = arr[1] = arr[1] = 2;
        // 1.2: arr[1] = temp = 1;
        // mark = 1; arr = [2,1,3,4];
        return arr;
        }
        ```
    * **C++**
        ```
        #include <bits/stdc++.h>

        using namespace std ;

        int main(){
        int A[1000000] ;
        int N , mark = 0 ; 
        
        cin >> N ;
        for(int i = 0 ; i < N ; i++ )
            cin >> A[i] ;  


        for (int i = 0 ; i < N ; i++)
            if( A[i] % 2 == 0 ){
                swap( A[mark] , A[i] ) ;
                mark++ ;
            }
        
        
        for (int i = 0 ; i < N ; i++)
            cout << A[i] << " " ;
        
        
            return 0 ;
        }
        ```
    * **Python**
        ```
        n = int(input())
        A = list(map(int, input().split()))

        mark = 0

        for i in range(n):
            if not A[i]%2:
                A[i], A[mark] = A[mark], A[i]
                mark += 1
        
        print(*A)
        ```