1，登录远程服务器
	ssh root@xxx	----> xxx 远程服务器ip地址

2，安装ShadowsocksR软件（如果没安装wget，则先执行该命令：yum -y install wget）
	wget --no-check-certificate https://freed.ga/github/shadowsocksR.sh; bash shadowsocksR.sh

补充：如果后面想查看SSR账号信息的话，输入以下命令即可。
	bash ssr.sh


class Solution {
    public int[] maxNumber(int[] nums1, int[] nums2, int k) {
        int[] newArr = new int[k];
        if(nums1.length + nums2.length < k){
            return newArr;
        }
        ArrManager arrManager1 = createMaxArr(nums1);
        ArrManager arrManager2 = createMaxArr(nums2);        
        
        return getMaxNumber(arrManager1, 0, arrManager2, 0, k);
    }

    public int[] getMaxNumber(ArrManager arrManager1, int start1, ArrManager arrManager2, int start2, int k){
        if(arrManager1)
    }

    public ArrManager createMaxArr(int[] arr){
        int len = arr.length - 1;
        int[] newArr = new int[arr.length];
        newArr[len] = len;
        for(int i = len - 1; i>=0; i--){
            int next = i+1;
            if(arr[i] < arr[next]){
                newArr[i] = next;
            } else {
                if(arr[i] >= arr[len]){
                    newArr[i] = i;
                    len = i;
                } else {
                    while(next < len && arr[i] >= arr[next]){
                        next++;
                    }
                    newArr[i] = next;
                }
            }
        }
        return new ArrManager(newArr, len);
    }

    class ArrManager{
        int[] arr;
        int maxIndex;
        public ArrManager(int[] arr, int maxIndex){
            this.arr = arr;
            this.maxIndex = maxIndex;
        }
    }
}
