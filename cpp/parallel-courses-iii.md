
  # parallel-courses-iii

  ```cpp
  class Solution {
public:
    int minimumTime(int n, vector<vector<int>>& A, vector<int>& time) {
        vector<vector<int>>adj(n);
        vector<int>indegree(n, 0);
        for(int i=0; i<A.size(); i++){
            adj[A[i][0]-1].push_back(A[i][1]-1);
            indegree[A[i][1]-1]++;
        }
        queue<int> q;
        vector<int> maxTime(n, 0);
        for(int i=0; i<n; i++){
            if(indegree[i]==0){
                q.push(i);
                maxTime[i]=time[i];
            }
        }
        while(!q.empty()){
            int node=q.front();
            q.pop();
            for(auto it: adj[node]){
                maxTime[it]=max(maxTime[it], maxTime[node]+time[it]);
                indegree[it]--;
                if(indegree[it]==0) q.push(it);
            }
        }
        int ans=0;
        for(int i=0; i<n; i++){
            ans=max(ans, maxTime[i]);
        }
        return ans;
    }
}; 
  ```
  