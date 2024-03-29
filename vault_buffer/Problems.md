# problem 1829

> \#todo

___

## Two Sum

<https://leetcode.com/problems/two-sum/>

```python
class Solution:
 def twoSum( self, param1, param2 ):
  return solution( param1, param2 )


def solution( nums, target ):
 memo = { }
 for i, el in enumerate( nums ):


  remaining = target - el
  if remaining in memo:
   prev_seen = memo[ remaining ]
   return [ prev_seen, i ]

  memo[ el ] = i

def naive( nums, target):
    for i in range( len( nums )):
        for j in range( i , len(nums)):
            if nums[i] + nums[j] == target:
                return [ i , j]

if __name__ == '__main__':
 import unittest


 class TestSolution( unittest.TestCase ):

  def test1( self ):
   self.assertEquals( solution( [ 2, 7, 11, 15 ], 9 ), [ 0, 1 ] )

  def test1( self ):
   self.assertEquals( solution( [ 3 , 2, 4 ], 6 ), [ 1 , 2  ] )


 unittest.main()

```

classic problem.
the naive solution is just brute forcew, with complexity O( n^2 ).
The better solution has linear complexity , and takes advantage of the complement / duality trick - "If the current number would be part of the answer, we know exactly what the other number would be. So the question becomes: given the current number, where (if any) have we seen the remaining difference?"

___

___
