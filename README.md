How-Many-IP-Address
===================

Given a digits Find out how many different IP address combinations are there ..



Given a string containing only digits, restore it by returning all possible valid IP address combinations.
For example:
Given "25525511135",
return ["255.255.11.135", "255.255.111.35"]{hint:recursion,backtrack}


Here is the Solution ...... 
it was taken me about 5 hours to solve see !!!

//cc Arun Kumar Gupta


import java.util.*;
public class AllIpAddress
{
    public static void main (String [] args)
    {
        Scanner sc = new Scanner(System.in);
        String input = sc.next();
        int[] intArray = new int[input.length()];
        int length = input.length();

        for (int i = 0; i < input.length(); i++) {
        intArray[i] = Character.digit(input.charAt(i), 10);
        //System.out.println(intArray[i]);
        }
        int i = 0 , j = 1 , k = 2;
        AllIpAddress ip = new AllIpAddress();
        ip.Ipaddress(intArray , i , j , k , length-1);    
        
        
        
    }
    void Ipaddress(int [] intArray , int i , int j , int k , int length)
    {
        try{
        int where = 0 ,change = 0;
        int p1 =createIP( intArray , -1 , i);
        int p2 =createIP( intArray , i ,  j );
        int p3 =createIP( intArray ,  j , k );
        int p4 =createIP( intArray ,  k ,  length );
        //System.out.println("**********Garbage"+p1+"."+p2+"."+p3+"."+p4);
        //System.out.println("i = "+i+"j = "+j+"k = "+k);
        if((p1<=255)&&(p2<=255)&&(p3<=255)&&(p4<=255)&&(p4>0))
        {
            System.out.println(p1+"."+p2+"."+p3+"."+p4);
        }
        if(p4 >255)
        {
            //if(k != j)
            //++k;
            where =4;
            //System.out.println("Problem at P4");
        }
        else if(p3>255)
        {
            //if(j != i)
            //++j;
            //--k;
            where = 3;
            //System.out.println("Problem at P3");
        }
        else if(p2>255)
        {
            //++i;
            where = 2;
            //System.out.println("Problem at P2");
        }
        else if(p1>255)
        {
            
            //System.out.println("Problem at P1");
            System.exit(0);
        }
        
        if((k == length) && (j+1 == k))
        {
            //System.out.println("if((k == length) && (j+1 == k))");
            //System.out.println(i+"_"+j+"_"+k);
            ++i;
            j = i+1;
            k = j+1;
            change = 1;
            //System.out.println(i+"_"+j+"_"+k);
            
        }
        if((k == length) &&(change == 0) )
        {
            //System.out.println("if((k == length) &&(change == 0) )");
            ++j;
            k = j+1;
            change = 0;
        }
        else if(change == 0)
        { 
            if( (k) < length )
            ++k;        
        }
        /*if(where ==4)
        { 
            ++k;            
        }
        if(where ==3)
        {
            ++j;
            --k;
        }
        if(where ==2)
        {
            ++i;
            --j;
        }
        /*if(k==length)
        {
            --k;
            --j;
        }*/
        Ipaddress(intArray , i , j , k , length);    
        }
        catch(ArrayIndexOutOfBoundsException e){
                 //System.out.println("Exception thrown  :" + e);
                      }
    }
    static int createIP(int [] intArray , int start , int end)
        {
            //System.out.println("I am at createIP()start = "+start+"\tend = "+end);
            int val = 1 , fina = 0;
            for(int e =end ; e>start ; --e)
            {
                 fina = intArray[e]*val + fina;  
                 val = val*10;
            }
            return fina;
        }
}
