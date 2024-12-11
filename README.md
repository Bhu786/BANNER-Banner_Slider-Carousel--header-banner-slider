# BANNER-Banner_Slider-Carousel--header-banner-slider



```react.js
import React, { useState, useEffect } from "react";
import banner1 from '../images/banner1.png';

const Slider = () => {
  // Array of slide data (images and text)
  const slides = [
    {
      id: 1,
      image: banner1, // Replace with your image URL
      heading: "BID VENCHURE",
      subheading: "Your Event, Their Best Offer!",
    },
    {
      id: 2,
      image: banner1, // Replace with your image URL
      heading: "PLAN YOUR EVENT",
      subheading: "Find the Best Venue!",
    },
    {
      id: 3,
      image: banner1, // Replace with your image URL
      heading: "EXPERIENCE MORE",
      subheading: "Save Big on Your Event Planning!",
    },
  ];

  const [currentSlide, setCurrentSlide] = useState(0);

  // Navigate to the next slide
  const nextSlide = () => {
    setCurrentSlide((prev) => (prev + 1) % slides.length);
  };

  // Navigate to the previous slide
  const prevSlide = () => {
    setCurrentSlide((prev) => (prev - 1 + slides.length) % slides.length);
  };

  // Set up the infinite timer
  useEffect(() => {
    const interval = setInterval(nextSlide, 3000); // Change slide every 3 seconds
    return () => clearInterval(interval); // Cleanup interval on component unmount
  }, []); // Empty dependency array ensures this runs once on mount

  return (
    <div className="relative w-full h-[60vh] overflow-hidden">
      {/* Slides */}
      {slides.map((slide, index) => (
        <div
          key={slide.id}
          className={`absolute top-0 left-0 w-full h-full transition-transform duration-700 ease-in-out ${
            index === currentSlide ? "translate-x-0" : "translate-x-full"
          }`}
          style={{
            backgroundImage: `url(${slide.image})`,
            backgroundSize: "cover",
            backgroundPosition: "center",
          }}
        >
          {/* Overlay */}
          <div className="bg-black bg-opacity-50 w-full h-full flex flex-col items-center justify-center text-center text-white px-4">
            <h1 className="text-4xl md:text-6xl font-bold">{slide.heading}</h1>
            <p className="text-lg md:text-2xl mt-4">{slide.subheading}</p>
          </div>
        </div>
      ))}

      {/* Navigation Buttons */}
      <button
        className="absolute top-1/2 left-5 transform -translate-y-1/2 bg-black bg-opacity-50 text-white p-3 rounded-full"
        onClick={prevSlide}
      >
        ❮
      </button>
      <button
        className="absolute top-1/2 right-5 transform -translate-y-1/2 bg-black bg-opacity-50 text-white p-3 rounded-full"
        onClick={nextSlide}
      >
        ❯
      </button>

      {/* Dots for Slide Navigation */}
      <div className="absolute bottom-5 left-1/2 transform -translate-x-1/2 flex gap-2">
        {slides.map((_, index) => (
          <button
            key={index}
            className={`w-3 h-3 rounded-full ${
              index === currentSlide ? "bg-white" : "bg-gray-400"
            }`}
            onClick={() => setCurrentSlide(index)}
          ></button>
        ))}
      </div>
    </div>
  );
};

export default Slider;
```
