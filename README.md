# Project
//package Lockmecom;

import java.util.*;

import java.io.*;

class Lockmecom implements Serializable{
   int pno;
   String pname;
   int price;

   Lockmecom(int pno, String pname, int price){
      this.pno = pno;
      this.pname = pname;
      this.price = price;
   }
   public String toString(){
      return pno+" "+pname+" "+price;
   }
}
class LockmecomDemo{
   public static void main(String[] args) throws Exception{
      int choice = -1;
      Scanner s = new Scanner(System.in);
      Scanner s1 = new Scanner(System.in);
      File file = new File("lockmecom.txt");
      ArrayList<Lockmecom> al = new ArrayList<Lockmecom>();
      ObjectOutputStream oos = null;
      ObjectInputStream ois = null;
      ListIterator li = null;
      if(file.isFile()){
         ois = new ObjectInputStream(new FileInputStream(file));
         al = (ArrayList<Lockmecom>)ois.readObject();
         ois.close();
      }
      do{
    	 System.out.println("LOCKME.COM MENU OPTIONS");
         System.out.println("1.INSERT");
         System.out.println("2.DISPLAY");
         System.out.println("3.SEARCH");
         System.out.println("4.DELETE");
         System.out.println("5.UPDATE");
         System.out.println("6.SORT By PNo - On Screen");
         System.out.println("7.SORT By PNo - In File");
         System.out.println("8.SORT By PName - On Screen");
         System.out.println("9.SORT By PName - In File");
         System.out.println("10.SORT By Price - Desc - On Screen");
         System.out.println("11.SORT By Price Asc - In File");
         System.out.println("0.EXIT");
         System.out.print("Enter Your Choice : ");
         choice = s.nextInt();

         switch(choice){
            case 1:
               System.out.println("Enter how many product you want : ");
               int n = s.nextInt();
               for(int i=0;i<n;i++){
                  System.out.print("Enter Product No: ");
                  int pno = s.nextInt();

                  System.out.print("Enter Product Name: ");
                  String pname = s1.nextLine();
                  
                  System.out.print("Enter Product Price : ");
                  int price = s.nextInt();

                  al.add(new Lockmecom(pno,pname,price));                 
               }
               oos = new ObjectOutputStream(new FileOutputStream(file));
               oos.writeObject(al);
               oos.close();
            break;
            case 2:
               if(file.isFile()){
                  ois = new ObjectInputStream(new FileInputStream(file));
                  al = (ArrayList<Lockmecom>)ois.readObject();
                  ois.close();

                  System.out.println("-------------------------------------");
                  li = al.listIterator();
                  while(li.hasNext())
                     System.out.println(li.next());
                  System.out.println("-------------------------------------");
               }else{
                  System.out.println("File not Exists....!");
               }
            break;
            case 3:
               if(file.isFile()){
                  ois = new ObjectInputStream(new FileInputStream(file));
                  al = (ArrayList<Lockmecom>)ois.readObject();
                  ois.close();

                  boolean found = false;
                  System.out.println("Enter pno to Search : ");
                  int pno = s.nextInt();
                  System.out.println("-------------------------------------");
                  li = al.listIterator();
                  while(li.hasNext()){
                     Lockmecom e = (Lockmecom)li.next();
                     if(e.pno == pno){
                        System.out.println(e);
                        found = true;
                     }
                  }
                  if(!found)
                     System.out.println("Record Not Found...!");
                  System.out.println("-------------------------------------");
               }else{
                  System.out.println("File not Exists....!");
               }
            break;          
            case 4:
               if(file.isFile()){
                  ois = new ObjectInputStream(new FileInputStream(file));
                  al = (ArrayList<Lockmecom>)ois.readObject();
                  ois.close();

                  boolean found = false;
                  System.out.print("Enter pno to Delete : ");
                  int pno = s.nextInt();
                  System.out.println("-------------------------------------");
                  li = al.listIterator();
                  while(li.hasNext()){
                     Lockmecom e = (Lockmecom)li.next();
                     if(e.pno == pno){
                        li.remove();
                        found = true;
                     }
                  }
                  if(found){
                     oos = new ObjectOutputStream(new FileOutputStream(file));
                     oos.writeObject(al);
                     oos.close();
                     System.out.println("Record Deleted Successfully....!");
                  }
                  else{
                     System.out.println("Record Not Found...!");                      
                  }
                  System.out.println("-------------------------------------");
               }else{
                  System.out.println("File not Exists....!");
               }
            break;          
            case 5:
               if(file.isFile()){
                  ois = new ObjectInputStream(new FileInputStream(file));
                  al = (ArrayList<Lockmecom>)ois.readObject();
                  ois.close();

                  boolean found = false;
                  System.out.print("Enter pno to Update : ");
                  int pno = s.nextInt();
                  System.out.println("-------------------------------------");
                  li = al.listIterator();
                  while(li.hasNext()){
                     Lockmecom e = (Lockmecom)li.next();
                     if(e.pno == pno){
                        System.out.print("Enter New Product Name : ");
                        String pname = s1.nextLine();

                        System.out.print("Enter new Price : ");
                        int price = s.nextInt();
                        li.set(new Lockmecom(pno,pname,price));
                        found = true;
                     }
                  }
                  if(found){
                     oos = new ObjectOutputStream(new FileOutputStream(file));
                     oos.writeObject(al);
                     oos.close();
                     System.out.println("Record Updated Successfully....!");
                  }
                  else{
                     System.out.println("Record Not Found...!");                      
                  }
                  System.out.println("-------------------------------------");
               }else{
                  System.out.println("File not Exists....!");
               }
            break;       
            case 6:
               if(file.isFile()){
                  ois = new ObjectInputStream(new FileInputStream(file));
                  al = (ArrayList<Lockmecom>)ois.readObject();
                  ois.close();

                  Collections.sort(al, new Comparator<Lockmecom>(){
                     public int compare(Lockmecom e1, Lockmecom e2){
                        return e1.pno - e2.pno;
                     }  
                  });    

                  System.out.println("-------------------------------------");
                  li = al.listIterator();
                  while(li.hasNext())
                     System.out.println(li.next());
                  System.out.println("-------------------------------------");
               }else{
                  System.out.println("File not Exists....!");
               }
            break; 
            case 7:
               if(file.isFile()){
                  ois = new ObjectInputStream(new FileInputStream(file));
                  al = (ArrayList<Lockmecom>)ois.readObject();
                  ois.close();

                  Collections.sort(al, new Comparator<Lockmecom>(){
                     public int compare(Lockmecom e1, Lockmecom e2){
                        return e1.pno - e2.pno;
                     }  
                  });    

                  oos = new ObjectOutputStream(new FileOutputStream(file));
                  oos.writeObject(al);
                  oos.close();

                  System.out.println("-------------------------------------");
                  li = al.listIterator();
                  while(li.hasNext())
                     System.out.println(li.next());
                  System.out.println("-------------------------------------");
               }else{
                  System.out.println("File not Exists....!");
               }
            break; 
            case 8:
               if(file.isFile()){
                  ois = new ObjectInputStream(new FileInputStream(file));
                  al = (ArrayList<Lockmecom>)ois.readObject();
                  ois.close();

                  Collections.sort(al, new Comparator<Lockmecom>(){
                     public int compare(Lockmecom e1, Lockmecom e2){
                        return e1.pname.compareTo(e2.pname);
                     }  
                  });    

                  System.out.println("-------------------------------------");
                  li = al.listIterator();
                  while(li.hasNext())
                     System.out.println(li.next());
                  System.out.println("-------------------------------------");
               }else{
                  System.out.println("File not Exists....!");
               }
            break; 
            case 9:
               if(file.isFile()){
                  ois = new ObjectInputStream(new FileInputStream(file));
                  al = (ArrayList<Lockmecom>)ois.readObject();
                  ois.close();

                  Collections.sort(al, new Comparator<Lockmecom>(){
                     public int compare(Lockmecom e1, Lockmecom e2){
                        return e1.pname.compareTo(e2.pname);
                     }  
                  });    

                  oos = new ObjectOutputStream(new FileOutputStream(file));
                  oos.writeObject(al);
                  oos.close();

                  System.out.println("-------------------------------------");
                  li = al.listIterator();
                  while(li.hasNext())
                     System.out.println(li.next());
                  System.out.println("-------------------------------------");
               }else{
                  System.out.println("File not Exists....!");
               }
            break; 
            case 10:
               if(file.isFile()){
                  ois = new ObjectInputStream(new FileInputStream(file));
                  al = (ArrayList<Lockmecom>)ois.readObject();
                  ois.close();

                  Collections.sort(al, new Comparator<Lockmecom>(){
                     public int compare(Lockmecom e1, Lockmecom e2){
                        return e2.price - e1.price;
                     }  
                  });    

                  System.out.println("-------------------------------------");
                  li = al.listIterator();
                  while(li.hasNext())
                     System.out.println(li.next());
                  System.out.println("-------------------------------------");
               }else{
                  System.out.println("File not Exists....!");
               }
            break; 
            case 11:
               if(file.isFile()){
                  ois = new ObjectInputStream(new FileInputStream(file));
                  al = (ArrayList<Lockmecom>)ois.readObject();
                  ois.close();

                  Collections.sort(al, new Comparator<Lockmecom>(){
                     public int compare(Lockmecom e1, Lockmecom e2){
                        return e1.price - e2.price;
                     }  
                  });    

                  oos = new ObjectOutputStream(new FileOutputStream(file));
                  oos.writeObject(al);
                  oos.close();

                  System.out.println("-------------------------------------");
                  li = al.listIterator();
                  while(li.hasNext())
                     System.out.println(li.next());
                  System.out.println("-------------------------------------");
               }else{
                  System.out.println("File not Exists....!");
               }
            break; 
         }
      }while(choice!=0); 
   }
}
