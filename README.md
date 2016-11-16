# Algorithm
public class BinarySearch {
    public static void main(String args[]){
        int[] array = {1,3,5,7,9,11,13};
        System.out.println(search(array,9));
    }
    public static int search(int array[], int x){
        int from = 0;
        int to = array.length - 1;

        while(from <= to){
            int middle = (from+to)/2;
            if(x < array[middle]){
                to = middle - 1;
            }else if(x > array[middle]){
                from = middle + 1;
            }else{
                return middle;
            }
        }

        return -1;
    }
}

public class CountSort {

    public static void main(String args[]){
        int[] input = {2,3,8,11,4,8};
        int[] output = new int[input.length];
        countSourt(input,output,11);

        for(int i=0; i<output.length; i++){
            System.out.print(output[i] + " ");
        }
    }

    public static void countSourt(int[] input, int[] output, int k){
        int[] countArray = new int[k+1];
        for(int i=0; i<k; i++){
            countArray[i] = 0;
        }

        for(int i=0; i<input.length;i++){
            countArray[input[i]]++;
        }

        for(int i=1; i<countArray.length;i++){
            countArray[i] = countArray[i] + countArray[i - 1];
        }

        for(int i=input.length-1; i>=0; i--){
            output[countArray[input[i]] - 1] = input[i];
            countArray[input[i]] --;
        }
    }
}

public class Flag {
    public static void main(String args[]){
        String[] colors = {"R","G","G","R","B","G","R","B","G"};
        arrangeFlag(colors);
        for(int i=0; i<colors.length;i++){
            System.out.print(colors[i]);
        }
    }

    public static void arrangeFlag(String[] colors){
        int begin=0;
        int current = 0;
        int end = colors.length - 1;
        ///RGGRBGRG
        while(current <= end){
            if(colors[current] == "R"){
                swap(colors,current,begin);
                begin++;
                current++;
            }else if(colors[current] == "G"){
                current++;
            }else{
                swap(colors,current,end);
                end --;
                current ++;
            }
        }
    }

    public static void swap(String[] colors, int from, int to){
        String temp = colors[from];
        colors[from] = colors[to];
        colors[to] = temp;
    }
}
public class FxiedSum {

    public static void main(String args[]){
        int[] nums ={2,4,6,9,3,1,7,5};
        int[] newNums = sort(nums,0,nums.length-1);

        for(int i=0; i<newNums.length; i++){
            System.out.print(newNums[i]);
        }
    }
    public static int[] sort(int[] nums, int from, int to){

        if(from < to){
            int midleIndex = (to + from)/2;
            int[] first = sort(nums,from,midleIndex);
            int[] second = sort(nums,midleIndex+1,to);

           return merge(first,second);
        }else{
            int[] temp = new int[1];
            temp[0] = nums[to];
            return temp;
        }

    }

    public static int[] merge(int[] first, int[] second) {
        int[] temp = new int[first.length + second.length];
        int i = 0;// 左指针
        int j = 0;// 右指针
        int k = 0;

        // 把较小的数先移到新数组中
        while (i < first.length && j < second.length) {
            if (first[i] < second[j]) {
                temp[k++] = first[i++];
            } else {
                temp[k++] = second[j++];
            }
        }

        // 把左边剩余的数移入数组
        while (i == first.length && j < second.length) {
            temp[k++] = second[j++];
        }

        while (i< first.length && j == second.length) {
            temp[k++] = first[i++];
        }

        return temp;
    }
}
public class KMP {
    // 0 1 2 3 4 5 6 7
    // a b a d a b c a
    // 0 1 1 1 1 2 3 1
    // n = 0  ------ p(0) = a --------prev= aft== null  -------- next(0)  =  0
    // n = 1  ------ p(1) = b --------prev= aft(1)= a     -------- next(1)  =  1
    // n = 2  ------ p(2) = a --------prev=a  aft = b     -------- next(1)  =  1
    // n = 3  ------ p(3) = b --------prev=a  aft = a     -------- next(1)  =  2
    public static void main(String args[]){
        String[] target = {"a","a","b","c","a","b","c","a","b","d"};
        String[] pattern = {"a","b","c","a","b","c","a","b","d"};
        int[] next = generateNextArray(pattern);
        int tl = target.length;
        int pl = pattern.length;
        int t_index=0;
        int p_index=0;
        while(t_index<tl && p_index<pl){
            if(target[t_index] == pattern[p_index]){
                t_index ++;
                p_index++;
            }else{
                t_index = t_index - next[p_index] ;
                p_index = 0;
            }
        }
        if(p_index == pl){
            System.out.println("find in " + (t_index - pl));
        }else{
            System.out.println("Not find");
        }
        for(int i=0;i<next.length;i++){
            System.out.print(next[i]);
        }
    }

    public static int[] generateNextArray(String[] pattern){
        int next[] = new int[pattern.length];

        int pre_index = -1;
        int aft_index = 0;
        next[0] = -1;
        while(aft_index <7){
            if(pre_index ==-1 || pattern[pre_index] == pattern[aft_index]){
                ++pre_index;
                ++aft_index;
                next[aft_index] = pre_index;
            }
          else{
                pre_index = next[pre_index];

            }
        }

        return next;
    }
}
public class ListOrder {
    public static void main(String args[]){
        String[] chars = {"a","b","c"};
        allOrder(chars,0,chars.length - 1);

    }

   public static void allOrder(String[] strs, int from, int end){
       if(from == end){
           for(int i=0; i<=end; i++){
               System.out.print(strs[i]);
           }
           System.out.println();
       }else{
           for(int i=from; i<= end; i++){
               String temp = strs[from];
               strs[from] = strs[i];
               strs[i] = temp;

               allOrder(strs,from+1,end);

               String temp2 = strs[from];
               strs[from] = strs[i];
               strs[i] = temp2;
           }
       }
   }


}
public class LongestPalindrome {

    String longest = "";

    public String longestPalindrome(String s) {
        for(int i = 0; i < s.length(); i++){
            //计算奇数子字符串
            helper(s, i, 0);
            //计算偶数子字符串
            helper(s, i, 1);
        }
        return longest;
    }

    private void helper(String s, int idx, int offset){
        int left = idx;
        int right = idx + offset;
        while(left>=0 && right<s.length() && s.charAt(left)==s.charAt(right)){
            left--;
            right++;
        }
        // 截出当前最长的子串
        String currLongest = s.substring(left + 1, right);
        // 判断是否比全局最长还长
        if(currLongest.length() > longest.length()){
            longest = currLongest;
        }
    }
}
public class Reverse {

    public static void main(String args[]){
        String[] letters = {"a","b","d","e"};
        print(letters);
        moveToEnd(letters,2);
        print(letters);
    }

    public static void reverse(String[] letters){
        int i = 0;
        int j = letters.length - 1;
        while(i<j){
            String temp = letters[i];
            letters[i] = letters[j];
            letters[j] = temp;

            i++;
            j--;
        }
    }

    public static void print(String[] letters){
        for(int index = 0; index < letters.length; index ++)
        System.out.print(letters[index]);

        System.out.println();
    }

    public static void moveToEnd(String[] letters, int movedSize){

        reverse(letters,0,movedSize-1);
        reverse(letters,movedSize,letters.length - 1);
        reverse(letters,0,letters.length - 1);
    }

    public static void reverse(String[] letters, int from, int to){
        while(from<to){
            String temp = letters[from];
            letters[from] = letters[to];
            letters[to] = temp;

            from++;
            to--;
        }
    }
}
public class Stage {
    public static void main(String args[]){
        System.out.println(calWayCount(3));
        System.out.println(calWayCount(4));
        System.out.println(calWayCount(5));
    }

    public static int calWayCount(int n){
        if(n==1){
            return 1;
        }else
        if(n==2){
            return 2;
        }else{
            return calWayCount(n-1) + calWayCount(n-2);
        }
    }
}
public class Sunday {
    public static void main(String args[]){
        String[] target =  {"a","c","b","c","a","b","c"};
        String[] pattern = {"a","b","c",};

        System.out.println(sunday(target,pattern));

    }

    public static int sunday(String[] target,String[] pattern){
        int tl = target.length;
        int pl = pattern.length;

        int t_index = 0;
        int p_index = 0;

        while(t_index < tl && p_index < pl){
            if(target[t_index] == pattern[p_index]){
                t_index ++;
                p_index ++;
            }else{
                int t_next_index = pl - p_index + t_index;
                String t_next = target[t_next_index];
                int t_next_position_in_pattern = contains(pattern,t_next);
                if(t_next_position_in_pattern >= 0){
                    t_index = pl - t_next_position_in_pattern + t_index;
                }else{
                    t_index += pl - p_index;
                }

                p_index = 0;
            }
        }

        if(p_index == pl){
            return t_index - pl;
        }else
            return -1;
    }

    public static int contains(String[] pattern, String t_next){
        for(int i=0;i < pattern.length;i++){
            if(pattern[i] == t_next){
                return i;
            }
        }
        return -1;
    }
}

