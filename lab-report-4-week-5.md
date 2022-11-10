# Lab Report 4 Week 5

## Alternative ways to use command line commands

> grep


* grep -i 

Using `-i` option with grep will grep the desired string from the file without requring the matching of uppercase and lowercase letters. If we did not use the `-i` option, the lines that contains "*This*" will not be displayed.

*Example 1:*

```
# input:
(base) justinliu@JustindeMacBook-Air skill-demo1 % grep -i "this" technical/plos/pmed.0020212.txt

# output:
        particularly regarding the molecular genetics of this complex disorder of mind and brain.
        progress in this historically difficult area of inquiry does not seem to be widely
        appreciated. The purpose of this article is to provide a high-level review of progress, its
        schizophrenia. A subset of this work is summarized in Figure 1. Of a large set of pre- and
        To summarize this literature briefly, schizophrenia is familial, or “runs” in families.
        and 4 linkage studies were 42%, 35%, 14%, 6%, and 3%, respectively. This crude summation
        This encouraging summation of work in progress masks a critical issue—the lack or
        current genes are true. This implies that the genetics of schizophrenia are different from
        replication elusive. The currently murky view of this literature may result from the
        This body of work is not yet ready for wholesale translation into clinical practice.
        However, it is not premature to inform patients that this work is advancing and that it
        genetic variation were proven to be causal to schizophrenia, this poor reflection might
```

As shown above, `grep -i this` found all the lines that either contains "this" or "This" and returned them. Even though it's not shown in here, it would grep something like "ThIs" and "tHIS" and etc as well since it's case free. 

*Example 2*

```
# input: 
(base) justinliu@JustindeAir skill-demo1 % grep -i "BiOmEd" technical/plos/pmed.0020212.txt

#output:
        Schizophrenia—like most other complex traits in biomedicine—has had a large number of
        other biomedical disorders. The alternative possibility is that the current findings are
```

As shown in this case, all lines that contain the word "biomed" in different case has been returned by `grep`.


#Example 3:#

```
# input:
(base) justinliu@JustindeAir skill-demo1 % grep -i "FINDING" technical/plos/pmed.0020212.txt

#output:
        findings, as summarized in Table 1 [9, 10].
        It is unlikely that all of these linkage findings are true. The regions suggested by the
        findings.
        findings provides further support; 3) mRNA from each gene is expressed in the prefrontal
        INS [22]; 2) for Type 2 diabetes mellitus, there are a number of findings
        multiple linkage studies. For these findings, the data are highly compelling and consistent
        possibilities. The first possibility is that the current findings for some of the best
        other biomedical disorders. The alternative possibility is that the current findings are
        but definitive answers are not yet fully established. Findings from the accumulated
        and false positive findings; however, it would be a momentous advance for the field if even
```

Once agian, we used `grep -i` to find all the lines containg "finding", ignoring the cases.

---

* grep -v

As we'll show later, `grep -v` will grep lines from a file with an inverted sense of matching, which means it will grep all the lines that does not contain the given keyword and return them to the user. This may be pretty useful to us sometime if we'd like to sift out some of the lines that we may not need in a file.

*Example 1:*

```
# input:
(base) justinliu@JustindeMacBook-Air skill-demo1 % grep  -v "a" technical/plos/pmed.0020212.txt 

# output:

  
    
      
        
      
      
      
      
        genes.
      
      
        studies.
        findings.
      
      
      
      
        Synthesis
        DISC1 , 
        DTNBP1 , 
        the involvement of 
        receptors. Moreover, 
        CAPN10 , 
        possibilities.
      
      
        improve [28].
      
    
  
```
As the above example shows, `grep -v` will selec all the lines that does not contain the given key word, which is "a" in this case as we provided. In addition, from this example we can see that `grep -v` will return many lines of empty lines since it's inverted selected, which may be a disadvantage sometime.

*Example 2:*

```
# input:
(base) justinliu@JustindeAir skill-demo1 % grep -v "e" technical/plos/pmed.0020212.txt

#output:
  
    
      
        
      
      
      
      
      
      
        findings.
      
      
      
      
        DISC1 , 
        DTNBP1 , 
        NRG1 , and 
        DTNBP1 and 
        CAPN10 , 
        KCNJ11 , and 
      
      
      
    
  
```
As we can see from this exmaple, again, `grep -v` may return many empty lines beside the useful lines we want, so we will try to take these empty lines out to make `grep -v` even more useful if we do not want to know how many empty lines there are.

*Example 3:*

```
# input:
(base) justinliu@JustindeAir skill-demo1 % grep -v "e" technical/plos/pmed.0020212.txt | grep -v '^[[:space:]]*$' 

# output:
        findings.
        DISC1 , 
        DTNBP1 , 
        NRG1 , and 
        DTNBP1 and 
        CAPN10 , 
        KCNJ11 , and 
```
This time, using pipe and `grep -v '^[[:space:]]*$'`, in whcih `'^[[:space:]]*$'` means blank spaces, we are allowed to grep all the lines that do not contain certain string while not getting the empty lines displayed. 

---

* grep -c

Appending `-c` to `grep` will make it only return the number of matching lines instead of displaying all the matching lines to the user. This may be more convenient if we only want to know the number of matching lines without wanting to know what are the contents of the matching lines.

*Example 1:*

```
# input:
(base) justinliu@JustindeMacBook-Air skill-demo1 % grep  -c "a" technical/plos/pmed.0020212.txt

# output:
167
```

As shown above, `grep -c` only returns how many lines contains the matching string, which makes the display much cleaner if all we want to know is the number of lines that matched.

*Example 2:*

```
#input:
(base) justinliu@JustindeAir skill-demo1 % grep  -c "e" technical/plos/pmed.0020212.txt

#output:
171

```

Once again, only the number of matches shows up.

*Example 3:*

```
#input:
(base) justinliu@JustindeAir skill-demo1 % grep  -c "i" technical/plos/pmed.0020212.txt

#output:
170
```
This may be very convenient sometime if we do not care about the matching contents.