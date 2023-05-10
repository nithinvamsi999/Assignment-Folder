#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

class Solution {
public:
    vector<int> bestCoordinate(vector<vector<int>>& towers, int radius) {
        int n = towers.size();
        int sum;
        int ans = 0;
        pair<int,int> ansCoor = make_pair(0, 0);

        for(int x = 0; x <= 50; x++){
            for(int y = 0; y <= 50; y++){
                sum = 0;
                for(const auto it : towers){
                    int xa = it[0];
                    int ya = it[1];
                    int qa = it[2];
                    int distance = (x - xa) * (x - xa) + (y - ya) * (y - ya);
                    if(distance > radius * radius) {
                        continue;
                    }
                    sum += (int)(qa / (1 + sqrt(double(distance))));
                }
                if(sum > ans){
                    ans = sum;
                    ansCoor = make_pair(x, y);
                }
            }
        }
        return vector<int>{{ansCoor.first, ansCoor.second}};
    }
};

int main() {
    int numTowers;
    cout << "Enter the number of towers: ";
    cin >> numTowers;

    vector<vector<int>> towers(numTowers);
    for (int i = 0; i < numTowers; i++) {
        int x, y, quality;
        cout << "Enter coordinates and quality of tower " << i + 1 << ": ";
        cin >> x >> y >> quality;
        towers[i] = {x, y, quality};
    }

    int radius;
    cout << "Enter the radius: ";
    cin >> radius;

    Solution s;
    vector<int> result = s.bestCoordinate(towers, radius);

    cout << "Best Coordinate: (" << result[0] << ", " << result[1] << ")" << endl;

    return 0;
}
