### 基本思路

贪就完了。

首先要明确的是，在任何时刻都须保证机器人之间的距离最近。

因此，当某一时刻一个机器人的横坐标（或纵坐标）小于另一个机器人时，需要增加横坐标（或纵坐标）；横坐标（或纵坐标）大于另一个机器人时，需要减少横坐标（或纵坐标）。

另外，题目中给到“都分配给两个机器人”这一条件，因此不能使机器人没有动过。

### 代码实现

```cpp
#include <bits/stdc++.h>
using namespace std;
int t;
int main(){
    cin >> t;
    while(t--){
        int n, x1, y1, x2, y2;
        bool f1 = 0, f2 = 0;
        string ans = "", s; 
        x1 = y1 = x2 = y2 = 1;
        s = ' ' + s;
        for(int i = 1; i <= n; i++){
            if(s[i] == 'N'){
                if(y1 > y2 || (y1 == y2 && !f2)){
                    y2++;
                    f2 = 1;
                    ans += 'H';
                }
                else{
                    y1++;
                    f1 = 1;
                    ans += 'R';
                }
            }
            else if(s[i] == 'S'){
                if(y1 > y2 || (y1 == y2 && !f1)){
                    y1--;
                    f1 = 1;
                    ans += 'R';
                }
                else{
                    y2--;
                    f2 = 1;
                    ans += 'H';
                }
            }
            else if(s[i] == 'E'){
                if(x1 > x2 || (x1 == x2 && !f2)){
                    x2++;
                    f2 = 1;
                    ans += 'H';
                }
                else{
                    x1++;
                    f1 = 1;
                    ans += 'R';
                }
            }
            else{
                if(x1 > x2 || (x1 == x2 && !f1)){
                    x1--;
                    f1 = 1;
                    ans += 'R';
                }
                else{
                    x2--;
                    f2 = 1;
                    ans += 'H';
                }
            }
        }
        if(x1 == x2 && y1 == y2 && f1 && f2) cout << ans;
        else cout << "NO";
        cout << '\n';
    }
    return 0;
}
```
