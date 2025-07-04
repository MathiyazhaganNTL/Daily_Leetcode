class Solution {
    public int minOperations(List<Integer> nums, int k) {
        int operation=0;
        List<Integer> a=new ArrayList<>();
        for (int i=1;i<=k;i++)
            a.add(i);
        
        for (int i=nums.size()-1;i>=0;i--)
        {
            if (a.contains(nums.get(i)))
                a.remove(nums.get(i));
            operation++;
            if (a.size()==0)
                break;
            
        }
        return operation;
    }
}
