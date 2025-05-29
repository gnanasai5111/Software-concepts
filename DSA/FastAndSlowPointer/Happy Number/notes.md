class Solution {
    public int getDigitSquareSum(int number) {
        int sum = 0;
        while (number > 0) {
            int digit = number % 10;
            sum += digit * digit;
            number /= 10;
        }
        return sum;
    }

    public boolean isHappy(int n) {
        int current = n;
        HashSet<Integer> seenSums=new HashSet<>();
        while(current!=1){
            current=getDigitSquareSum(current);
            if (seenSums.contains(current)) {
                return false;
            }
            seenSums.add(current);
        }  
        return true;
        
    }
}
