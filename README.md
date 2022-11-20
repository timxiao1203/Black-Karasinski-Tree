# Black-Karasinski Short Rate Tree Algorithm

The Black-Karasinski model is a short rate model that assumes the short-term interest rates to be log-normally distributed. We implement the one factor  Black-Karasinski model as a binomial or trinomial tree.

Assume that short term interest rate process,  , satisfies, under the risk neutral probability measure, a SDE of Black-Karasinski form,

 

where  

•	  denotes standard Brownian motion,
•	  is the volatility, 
•	 , with  ,  is the mean reversion,
•	  is chosen to match the initial term structure of zero coupon bond prices.

Our approach towards building a tree for the short-term interest rate process,  ,  is based on the single-factor tree construction technique.   Specifically let 

 , 

where the process   satisfies the SDE

 				(2.1)

Then 

 

where  .  We first build a tree for the process   as described below.   

Let  .  From Ito’s Lemma,

 ,
 

Then

 

where  .  

Next let

 ,

where   and  , be a partition of the interval  ; furthermore, let   be an additional time slice. We can view our tree for the process   as a directed graph, which is defined by a set of vertices and directed edges.  Let   and  , for  , respectively denote a tree node at time slice   and the associated value for  ; here  , for  , denotes the total  number of nodes on the   time slice.  Furthermore let 

 

denote the random variable  

 

where   .   Then 

 .

Since 

 

Then

 

We build a tree for  , based on Myint’s equity tree construction technique, using the expressions above for   and  .  Here we employ a partition with spacing of 

 

at time slice  , for  , where  

Let  , for   and  , denote a child, at the   time slice, of the tree node  ; here   denotes the number of children emanating from the parent node,   (e.g.,   for a trinomial tree).   Let  , for   and  , denote the price at time zero of an Arrow-Debreu security at the node  , that is, a security that pays 1 currency unit if the node   is reached at time   and zero otherwise. 

Black-Karasinski short rate tree approach can be used to price convertible bond. Convertible bond is not only a coupon paying bond (see https://finpricing.com/lib/FiBond.html) but also can be converted at the discretion of the holder within the periods of time specified by the conversion schedule. Typically, the issuer has the option to buy the bond back at a predetermined strike price(s) during the callable period(s). Also, there are provisions that allow the holder to return the bond to the issuer in exchange for a predetermined cash price during certain period(s). 

Let   denote the price at time zero of a zero coupon bond with maturity of   and face value of 1 currency unit.  We determine  at each time slice by matching the initial term structure of zero coupon bond prices.  We first solve 

 

for  , that is,  .  We then set the Arrow-Debreu security values at the time slice   to

 

for  , where   denotes the tree root node.

For  ,  let

 

Sequentially, for  , we then numerically solve

 					(1)

for the unknown  .   Here we employ the Newton iteration scheme

  ,

for  .  Observe that

 

which we denote by  .   An initial guess to the Newton iteration scheme above,  , is then obtained by solving

 

for the unknown  ; that is, 

 .



