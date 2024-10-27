
public class RideRequest {
	
	 
    private String customerName;
    private String rideDetails;
    private double ridePrice;
    private boolean hasDiscount;
    private static double taxrate;
    private static double discount;
    private static int toStringCounter;

    public RideRequest() {
    	
        this.customerName = "";
        this.rideDetails = "";
        this.ridePrice = 0.0;
        this.hasDiscount = false;
      
    
    }

    public RideRequest(RideRequest request) {
        if (request == null) {
            throw new IllegalArgumentException("Request object cannot be null");
        }
       
        	  this.customerName = request.customerName;
              this.rideDetails = request.rideDetails;
              this.ridePrice = request.ridePrice;
              this.hasDiscount = request.hasDiscount;
       
    }

    public RideRequest(String request) {
        if (request == null || request.trim().isEmpty()) {
            throw new IllegalArgumentException("Input request cannot be null or empty");
        }
       
        String[] part = request.split(",");
        if (part.length != 4) {
            throw new IllegalArgumentException("Input request must be in the format: 'name, location, price, discount'");
        }
        this.customerName = part[0].trim();
        this.rideDetails = part[1].trim();
        try {
            this.ridePrice = Double.parseDouble(part[2].trim());
        } catch (NumberFormatException e) {
            throw new IllegalArgumentException("Invalid price format in request");
        }
        
        this.hasDiscount = part[3].trim().equalsIgnoreCase("Y");
    
    }

    public void setCustomerName(String customerName) {
        this.customerName = customerName;
    }

    public String getCustomerName() {
        if (this.customerName == null || this.customerName.equals("")) {
            return "";
        }
        if (this.customerName.length() > 10) {
            return "Very Long ";
        }
        return customerName;
    }

    public void setRidePrice(double ridePrice) {
        this.ridePrice = ridePrice;
    }

    public double getRidePrice() {
        return ridePrice;
    }

    public void setHasDiscount(boolean hasDiscount) {
        this.hasDiscount = hasDiscount;
    }

    public boolean isHasDiscount() {
        return hasDiscount;
    }

    public void setRideDetails(String rideDetails) {
    	  if (rideDetails != null) {
    	        this.rideDetails = rideDetails.trim();
    	    } else {
    	        this.rideDetails = "";
    	    }
    }

    public String getRideDetails() {
        if (this.rideDetails == null || this.rideDetails.equals("")) {
            return "";
        } else {
            return rideDetails;
        }
    }

    public static void setTaxrate(double taxrate) {
        RideRequest.taxrate = taxrate;
    }

    public static double getTaxrate() {
        return taxrate;
    }

    public static void setDiscount(double discount) {
        RideRequest.discount = discount;
    }

    public static double getDiscount() {
        return discount;
    }
    public static void setToStringCounter(int toStringCounter) {
        RideRequest.toStringCounter = toStringCounter;
    }
    public static int getToStringCounter() {
        return toStringCounter;
    }

    public String toString() {
    	    toStringCounter++;
    	    double priceWithTax = ridePrice + (ridePrice * taxrate);
    	    double finalPrice = priceWithTax;
    	    
    	    if (hasDiscount) {
    	        finalPrice -= priceWithTax * discount;
    	        return String.format(" %d. %-10s|%-25s|%-12.2f|%13.2f",
    	            toStringCounter, customerName, rideDetails, priceWithTax, finalPrice);
    	    } else {
    	        return String.format(" %d. %-10s|%-25s|%-12.2f|", 
    	            toStringCounter, customerName, rideDetails, priceWithTax);
    	    }
    }
}
