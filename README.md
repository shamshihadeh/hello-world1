using System;

namespace ClassLibrary
{
    public class clsOrder
    {
        //private data member for the OrderID property
        public Int32 mOrderID;
        public DateTime mOrderDate;
        public Boolean mDispatch;
        public string mComments;
        public Double mPrice;

      
        public int OrderID {
            get
            {
                //sends data out of the property
                return mOrderID; 
            }

            set
            {
                //allows the data into the property
                mOrderID = value;
            }
       }


        public DateTime OrderDate { 
            get
            {
                return mOrderDate;
            }
            set
            {
                mOrderDate = value;
            }
        
        }


        public Boolean Dispatch { 
            get
            {

                return mDispatch;

            }
            set
            {

                mDispatch = value;

            } 
               }
        
        
        public string Comments { 
            get
            {
                return mComments;
            }
                set
            {
                mComments = value;
            }
        }


        public Double Price {
            get
            {
                return mPrice;
            
            }
            set
            {
                mPrice = value;
            }  
                
           }

        public bool Find(int orderID)
        {

            //create an instance of the data connection 
            clsDataConnection DB = new clsDataConnection();
            //add the parameter for the orderID to search for 
            DB.AddParameter("orderID", orderID);
            //execute the stored procedure 
            DB.Execute("sproc_tblOrder_FilterByOrderID");
            //if one record is found (there should be tiether one or zero)
            if (DB.Count == 1)
            {
                mOrderID = Convert.ToInt32(DB.DataTable.Rows[0]["OrderID"]);
                mOrderDate = Convert.ToDateTime(DB.DataTable.Rows[0]["OrderDate"]);
                mDispatch = Convert.ToBoolean(DB.DataTable.Rows[0]["Dispatch"]);
                mComments = Convert.ToString(DB.DataTable.Rows[0]["Comments"]);
                mPrice = Convert.ToDouble(DB.DataTable.Rows[0]["Price"]);
                //return that everything worked OK
                return true;
            }
            //if no record was found 
            else 
            {
            //return false indicating a problem
            return false;
            }

        }
    }
}
