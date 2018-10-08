<script type="text/javascript"
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
##<center>Compiler HomeWork3</center>
###<p align="right">151220137 许子谦</p>

###Ex4.4.1-5)
S -> (L) | a  
L -> L,S | S  
该文法无左公因子，但有左递归，需消除  
消除左递归即把 A -> Aα | β 替换为 A -> βA' 和 A' -> αA' | ϵ  
消除左递归得  

```
S -> (L) | a
L -> SL'
L' -> ,SL' | ϵ
```

FIRST && FOLLOW 集合

```
FIRST(S)={(, a}
FIRST(L)={(, a}
FIRST(L')={',', ϵ}

FOLLOW(S)={$, ',', ϵ, )}//FIRST(L')+FOLLOW(L')+$
FOLLOW(L)={$, )}//似乎没有$??下面也是
FOLLOW(L')={$, )}//FOLLOW(L)
```


####预测分析表

<table>
   <thead>
    <tr>
        <td rowspan="2">非终结符号</td>
        <td colspan="6">输入符号</td>  
    </tr>
    <tr>
        <td>(</td>
        <td>)</td>
        <td>a</td>
        <td>,</td>
        <td>ϵ</td>
        <td>$</td>
    </tr>
  </thead>
    <tr>
        <td>L</td>
        <td>S -> (L)</td>
        <td></td>
        <td>S -> a</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>L</td>
        <td>L -> SL'</td>
        <td></td>
        <td>L -> SL'</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>L'</td>
        <td></td>
        <td>L' -> ϵ</td>
        <td></td>
        <td>L' -> ,SL'</td>
        <td></td>
        <td>L' -> ϵ</td>
    </tr>
</table>




####步骤

<table>
    <tr>
        <td>已匹配</td>
        <td>栈</td>
        <td>输入</td>
        <td>动作</td>
    </tr>
    <tr>
        <td></td>
        <td align="right">S$</td>
        <td align="right">((a,a),a,(a))$</td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td align="right">(L)$</td>
        <td align="right">((a,a),a,(a))$</td>
        <td>输出S -> (L)</td>
    </tr>
    <tr>
        <td>(</td>
        <td align="right">L)$</td>
        <td align="right">(a,a),a,(a))$</td>
        <td>匹配(</td>
    </tr>
    <tr>
        <td>(</td>
        <td align="right">SL')$</td>
        <td align="right">(a,a),a,(a))$</td>
        <td>输出 L -> SL'</td>
    </tr>
    <tr>
        <td>(</td>
        <td align="right">(L)L')$</td>
        <td align="right">(a,a),a,(a))$</td>
        <td>输出S -> (L)</td>
    </tr>
    <tr>
        <td>((</td>
        <td align="right">L)L')$</td>
        <td align="right">a,a),a,(a))$</td>
        <td>匹配(</td>
    </tr>
    <tr>
        <td>((</td>
        <td align="right">SL')L')$</td>
        <td align="right">a,a),a,(a))$</td>
        <td>输出 L -> SL'</td>
    </tr>
    <tr>
        <td>((</td>
        <td align="right">aL')L')$</td>
        <td align="right">a,a),a,(a))$</td>
        <td>输出S -> a</td>
    </tr>
    <tr>
        <td>((a</td>
        <td align="right">L')L')$</td>
        <td align="right">,a),a,(a))$</td>
        <td>匹配a</td>
    </tr>
    <tr>
        <td>((a</td>
        <td align="right">,SL')L')$</td>
        <td align="right">,a),a,(a))$</td>
        <td>输出 L' -> ,SL'</td>
    </tr>
    <tr>
        <td>((a,</td>
        <td align="right">SL')L')$</td>
        <td align="right">a),a,(a))$</td>
        <td>匹配,</td>
    </tr>
    <tr>
        <td>((a,</td>
        <td align="right">aL')L')$</td>
        <td align="right">a),a,(a))$</td>
        <td>输出S -> a</td>
    </tr>
    <tr>
        <td>((a,a</td>
        <td align="right">L')L')$</td>
        <td align="right">),a,(a))$</td>
        <td>匹配a</td>
    </tr>
    <tr>
        <td>((a,a</td>
        <td align="right">)L')$</td>
        <td align="right">),a,(a))$</td>
        <td>输出L -> ϵ</td>
    </tr>
    <tr>
        <td>((a,a)</td>
        <td align="right">L')$</td>
        <td align="right">,a,(a))$</td>
        <td>匹配)</td>
    </tr>
    <tr>
        <td>((a,a)</td>
        <td align="right">,SL')$</td>
        <td align="right">,a,(a))$</td>
        <td>输出 L' -> ,SL'</td>
    </tr>
    <tr>
        <td>((a,a),</td>
        <td align="right">SL')$</td>
        <td align="right">a,(a))$</td>
        <td>匹配,</td>
    </tr>
    <tr>
        <td>((a,a),</td>
        <td align="right">aL')$</td>
        <td align="right">a,(a))$</td>
        <td>输出S -> a</td>
    </tr>
    <tr>
        <td>((a,a),a</td>
        <td align="right">L')$</td>
        <td align="right">,(a))$</td>
        <td>匹配a</td>
    </tr>
    <tr>
        <td>((a,a),a</td>
        <td align="right">,SL')$</td>
        <td align="right">,(a))$</td>
        <td>输出 L' -> ,SL'</td>
    </tr>
    <tr>
        <td>((a,a),a,</td>
        <td align="right">SL')$</td>
        <td align="right">(a))$</td>
        <td>匹配,</td>
    </tr>
    <tr>
        <td>((a,a),a,</td>
        <td align="right">(L)L')$</td>
        <td align="right">(a))$</td>
        <td>输出S -> (L)</td>
    </tr>
    <tr>
        <td>((a,a),a,(</td>
        <td align="right">L)L')$</td>
        <td align="right">a))$</td>
        <td>匹配(</td>
    </tr>
    <tr>
        <td>((a,a),a,(</td>
        <td align="right">SL')L')$</td>
        <td align="right">a))$</td>
        <td>输出 L -> SL'</td>
    </tr>
    <tr>
        <td>((a,a),a,(</td>
        <td align="right">aL')L')$</td>
        <td align="right">a))$</td>
        <td>输出S -> a</td>
    </tr>
    <tr>
        <td>((a,a),a,(a</td>
        <td align="right">L')L')$</td>
        <td align="right">))$</td>
        <td>匹配a</td>
    </tr>
    <tr>
        <td>((a,a),a,(a</td>
        <td align="right">)L')$</td>
        <td align="right">))$</td>
        <td>输出L -> ϵ</td>
    </tr>
    <tr>
        <td>((a,a),a,(a)</td>
        <td align="right">L')$</td>
        <td align="right">)$</td>
        <td>匹配)</td>
    </tr>
    <tr>
        <td>((a,a),a,(a)</td>
        <td align="right">)$</td>
        <td align="right">)$</td>
        <td>输出L -> ϵ</td>
    </tr>
    <tr>
        <td>((a,a),a,(a))</td>
        <td align="right">$</td>
        <td align="right">$</td>
        <td>匹配)</td>
    </tr>
</table>


####推导序列
\\(  S=>(L)=>L)=>SL')=>(L)L')=>L)L')=>SL')L')=>aL')L')=>L')L')=>,SL')L')=>... \\)  
\\(  SL')L')=>aL')L')=>L')L')=>)L')=>L')=>,SL')=>SL')=>aL')=>... \\)  
\\(  L')=>,SL')=>SL')=>(L)L')=>L)L')=>SL')L')=>aL')L')=>L')L')=>)L')=>L')=>) \\)  



---

###补充题
文法 E -> E+E | E*E | (E) | id  
有左公因子，也有左递归  
先提取左公因子  

```
E -> EE' | (E) | id  
E' -> +E | *E  
```

再消除左递归   

```
E -> (E)A' | idA'   
A' -> E'A' | ϵ  
E' -> +E | *E  
```

如果先消除左递归，再提取左公因子：（这时看不出还有左公因子了）   

```
E -> (E)A' | idA'   
A' -> +EA' | *EA' | ϵ
```


FIRST && FOLLOW 集合

```
FIRST(E)={(, id}
FIRST(A')={+, *, ϵ}
FIRST(E')={+, *]

FOLLOW(E)={$, (, +, *}//$+)+FOLLOW(E')
FOLLOW(A')={$, (, +, *}//FOLLOW(A)+FOLLOW(E)
FOLLOW(E')={$, (, +, *}//FIRST(A')-ϵ+FOLLOW(A)
```

<table>
    <tr>
        <td rowspan="2">非终结符号</td>
        <td colspan="7">输入符号</td>          
    </tr>
    <tr>
        <td>(</td>
        <td>)</td>
        <td>+</td>
        <td>*</td>
        <td>id</td>
        <td>ϵ</td>
        <td>$</td>
    </tr>
    <tr>
        <td>E</td>
        <td>E -> (E)A' </td>
        <td></td>
        <td></td>
        <td></td>
        <td>E -> idA' </td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>A'</td>
        <td></td>
        <td>A' -> ϵ </td>
        <td>A' -> E'A' | ϵ</td>
        <td>A' -> E'A' | ϵ</td>
        <td></td>
        <td></td>
        <td>A' -> ϵ </td>
    </tr>
    <tr>
        <td>E'</td>
        <td></td>
        <td></td>
        <td>E' -> +E</td>
        <td>E' -> *E</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
</table>

可见存在冲突，原来原文法本就是有二义性的，比如输入串id+id\*id时有两个最左推导序列：  
E=>E+E=>E+E\*E=>...=>id+id\*id  
E=>E\*E=>E+E\*E=>...=>id+id\*id  
为了解决这个二义性问题，在读入'\*'时，选择产生式 A' -> E'A'，选择A' -> ϵ 一定是错的  
为了解决这个二义性问题，在读入'+'时，选择产生式 A' -> ϵ 来降低优先级    

<table>
    <tr>
        <td rowspan="2">非终结符号</td>
        <td colspan="7">输入符号</td>          
    </tr>
    <tr>
        <td>(</td>
        <td>)</td>
        <td>+</td>
        <td>*</td>
        <td>id</td>
        <td>ϵ</td>
        <td>$</td>
    </tr>
    <tr>
        <td>E</td>
        <td>E -> (E)A' </td>
        <td></td>
        <td></td>
        <td></td>
        <td>E -> idA' </td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>A'</td>
        <td></td>
        <td>A' -> ϵ </td>
        <td>A' -> E'A'</td>
        <td>A' -> ϵ</td>
        <td></td>
        <td></td>
        <td>A' -> ϵ </td>
    </tr>
    <tr>
        <td>E'</td>
        <td></td>
        <td></td>
        <td>E' -> +E</td>
        <td>E' -> *E</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
</table>