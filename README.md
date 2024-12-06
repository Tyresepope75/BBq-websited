# BBq-website
import javafx.application.Application;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.scene.layout.*;
import javafx.stage.Stage;

public class GusStoreApp extends Application {
    
    // ObservableList to simulate a cart
    private ObservableList<String> cart = FXCollections.observableArrayList();
    private ListView<String> cartListView = new ListView<>(cart);
    private Label cartCountLabel = new Label("Items in Cart: 0");
    
    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        // Main layout
        BorderPane root = new BorderPane();
        
        // Banner at the top
        Label banner = new Label("Gus’s Outdoor BBQ and Ninja Equipment Emporium (and Space Rockets and Plumbing Specialist)");
        banner.setStyle("-fx-font-size: 24px; -fx-font-weight: bold;");
        root.setTop(banner);
        
        // BBQ Section
        VBox bbqSection = createBBQSection();
        // Ninja Equipment Section
        VBox ninjaSection = createNinjaSection();
        
        // Cart Section (bottom area)
        VBox cartSection = createCartSection();
        
        // Left layout for BBQ and Ninja Sections
        HBox center = new HBox(20, bbqSection, ninjaSection);
        root.setCenter(center);
        
        // Set the cart section to the bottom
        root.setBottom(cartSection);
        
        // Set the scene
        Scene scene = new Scene(root, 800, 600);
        primaryStage.setTitle("Gus's Store");
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    // BBQ section setup
    private VBox createBBQSection() {
        VBox bbqSection = new VBox(10);
        bbqSection.setStyle("-fx-padding: 10;");

        // Add BBQ items
        bbqSection.getChildren().add(new Label("BBQ Section"));
        bbqSection.getChildren().add(createBBQItem("BBQ Ribs", "A delicious rack of ribs!", "bbq_ribs.jpg"));
        bbqSection.getChildren().add(createBBQItem("Pulled Pork", "Slow cooked to perfection!", "pulled_pork.jpg"));
        bbqSection.getChildren().add(createBBQItem("BBQ Chicken", "Grilled and juicy!", "bbq_chicken.jpg"));
        
        // Fake Yelp Review
        Label review = new Label("Yelp Review: 6/5 stars! - Best BBQ ever!");
        bbqSection.getChildren().add(review);
        
        return bbqSection;
    }

    // Creates each BBQ item with a button to add to the cart
    private HBox createBBQItem(String name, String description, String imagePath) {
        HBox itemBox = new HBox(10);
        itemBox.setStyle("-fx-padding: 10;");

        // Item Image
        ImageView imageView = new ImageView(new Image(getClass().getResource(imagePath).toString()));
        imageView.setFitHeight(100);
        imageView.setFitWidth(100);
        
        // Item description
        VBox textBox = new VBox(5);
        textBox.getChildren().add(new Label(name));
        textBox.getChildren().add(new Label(description));

        // Add to Cart Button
        Button addButton = new Button("Add to Cart");
        addButton.setOnAction(e -> {
            cart.add(name);
            cartCountLabel.setText("Items in Cart: " + cart.size());
        });

        itemBox.getChildren().addAll(imageView, textBox, addButton);
        return itemBox;
    }

    // Ninja section setup
    private VBox createNinjaSection() {
        VBox ninjaSection = new VBox(10);
        ninjaSection.setStyle("-fx-padding: 10;");

        // Add Ninja items
        ninjaSection.getChildren().add(new Label("Ninja Equipment Section"));
        ninjaSection.getChildren().add(createNinjaItem("Ninja Sword", "Sharp and quick!", "ninja_sword.jpg"));
        ninjaSection.getChildren().add(createNinjaItem("Shuriken", "Perfect for stealthy attacks.", "shuriken.jpg"));
        ninjaSection.getChildren().add(createNinjaItem("Ninja Mask", "For when you need to be incognito.", "ninja_mask.jpg"));

        // Ninja Tip of the Day
        Label ninjaTip = new Label("Ninja Tip of the Day: Always stay hidden in the shadows!");
        ninjaSection.getChildren().add(ninjaTip);

        return ninjaSection;
    }

    // Creates each Ninja item with a button to add to the cart
    private HBox createNinjaItem(String name, String description, String imagePath) {
        HBox itemBox = new HBox(10);
        itemBox.setStyle("-fx-padding: 10;");

        // Item Image
        ImageView imageView = new ImageView(new Image(getClass().getResource(imagePath).toString()));
        imageView.setFitHeight(100);
        imageView.setFitWidth(100);
        
        // Item description
        VBox textBox = new VBox(5);
        textBox.getChildren().add(new Label(name));
        textBox.getChildren().add(new Label(description));

        // Add to Cart Button
        Button addButton = new Button("Add to Cart");
        addButton.setOnAction(e -> {
            cart.add(name);
            cartCountLabel.setText("Items in Cart: " + cart.size());
        });

        itemBox.getChildren().addAll(imageView, textBox, addButton);
        return itemBox;
    }

    // Cart Section setup
    private VBox createCartSection() {
        VBox cartSection = new VBox(10);
        cartSection.setStyle("-fx-padding: 10;");

        // Cart List and total count
        cartSection.getChildren().add(new Label("Your Cart:"));
        cartListView.setPrefHeight(150);
        cartSection.getChildren().add(cartListView);
        cartSection.getChildren().add(cartCountLabel);
        
        return cartSection;
    }
}
