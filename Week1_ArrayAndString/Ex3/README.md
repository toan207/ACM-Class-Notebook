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