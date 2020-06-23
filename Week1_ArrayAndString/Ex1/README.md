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