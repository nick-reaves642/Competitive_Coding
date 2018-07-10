```java
    private static void permutation(String str, String prefix, int lengthOfPermutationString) { //for strings
        if (prefix.length() == lengthOfPermutationString) {
                System.out.println(prefix);
            } else {
                for (int i = 0; i < str.length(); i++) {
                    permutation(str, prefix + str.charAt(i), lengthOfPermutationString);
                }
            }
        }

    private static void permutation(ArrayList<Integer> arr,ArrayList<Integer> res, int length){ //for arrays
        if (length==res.size()) {
            for (Integer x : res)
                System.out.print(x + " ");
            System.out.println();
        }
        else {
            for (int i = 0; i < arr.size(); i++) {
                res.add(arr.get(i));
                permute(arr, res, length);
                res.remove(res.size() - 1);
            }
        }

```
> **Note:** Code written in Java
