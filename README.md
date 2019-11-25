1，登录远程服务器
	ssh root@xxx	----> xxx 远程服务器ip地址

2，安装ShadowsocksR软件（如果没安装wget，则先执行该命令：yum -y install wget）
	wget --no-check-certificate https://freed.ga/github/shadowsocksR.sh; bash shadowsocksR.sh

补充：如果后面想查看SSR账号信息的话，输入以下命令即可。
	bash ssr.sh

int[] newArr;
    public int[] maxNumber(int[] nums1, int[] nums2, int k) {
        newArr = new int[k];
        ArrManager arrManager1 = createMaxArr(nums1); 
        ArrManager arrManager2 = createMaxArr(nums2); 
        return getFinalResult(arrManager1, nums1, arrManager2, nums2, k);
    }

    public int[] getFinalResult(ArrManager arrManager1, int[] nums1, ArrManager arrManager2, int[] nums2, int k){
        int[] result = {0};
        for(int i = Math.min(nums1.length, k); i >= 0; i--){
            int[] arrNum1 = getMaxNumber(arrManager1, nums1, i);
            int[] arrNum2 = getMaxNumber(arrManager2, nums2, k - i);
            int[] res = mergeArr(arrNum1,arrNum2);
            res = compareTo(res, result);
            
        }
        return result;
        
    }

    public int[] compareTo(int[] nums1, int[] nums2){

    }

    public int[] mergeArr(int[] nums1, int[] nums2){
        
    }

    public int[] getMaxNumber(ArrManager arrManager, int[] nums, int size){
        if(size == 0){
            return new int[0];
        }
        int[] arr = new int[size];
        int start = 0;
        if(nums.length - arrManager.maxIndex >= size){
            //代表maxIndex可以作为左边开始的第一位数
            arr[start++] = nums[arrManager.maxIndex];
            int index = arrManager.maxIndex + 1;
            while(index < nums.length){
                if(arrManager.arr[index] == index || (nums.length - arrManager.arr[index] >= size - start)){
                    arr[start++] = nums[arrManager.arr[index]];
                    index = arrManager.arr[index] + 1;
                } else {
                    arr[start++] = nums[index];
                    index++;
                }
            }
        } else {
            //代表maxIndex只能作为左边开始的第二位后面的数
            LinkedList<Integer> lst = new LinkedList<>();
            int leftNum = size - (nums.length - arrManager.maxIndex);
            int index = 0;
            while(index < arrManager.maxIndex){
                lst.addLast(nums[index]);
                if(lst.size() > length){
                    lst.poll();
                }
                if(arrManager.arr[index] == index){
                    index++;
                } else {
                    index = arrManager.arr[index];
                }
            }

            while(!lst.isEmpty()){
                arr[start++] = lst.poll();
            }
            arr[start++] = nums[arrManager.maxIndex];

            index = arrManager.maxIndex + 1;
            while(index < nums.length){
                arr[start++] = nums[index++];
            }
            
        }
        return arr;
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
