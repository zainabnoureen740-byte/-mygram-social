import React, { useState } from "react";
import { Heart, MessageCircle, Plus, User } from "lucide-react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";

export default function InstaClone() {
  const [posts, setPosts] = useState([
    {
      id: 1,
      user: "ali",
      image: "https://images.unsplash.com/photo-1520975916090-3105956dac38",
      caption: "Beautiful day 🌸",
      likes: 12,
      liked: false,
    },
    {
      id: 2,
      user: "zara",
      image: "https://images.unsplash.com/photo-1520975682031-a9ce5b7c7b1b",
      caption: "Nature vibes 🌿",
      likes: 30,
      liked: false,
    },
  ]);

  const toggleLike = (id) => {
    setPosts((prev) =>
      prev.map((p) =>
        p.id === id
          ? {
              ...p,
              liked: !p.liked,
              likes: p.liked ? p.likes - 1 : p.likes + 1,
            }
          : p
      )
    );
  };

  return (
    <div className="max-w-md mx-auto bg-white min-h-screen">
      {/* Header */}
      <div className="flex justify-between items-center p-4 border-b">
        <h1 className="text-xl font-bold">MyGram Social</h1>
        <Plus className="w-6 h-6" />
      </div>

      {/* Posts */}
      {posts.map((post) => (
        <Card key={post.id} className="my-4">
          <CardContent className="p-0">
            <div className="flex items-center p-3 gap-2">
              <User className="w-5 h-5" />
              <p className="font-semibold">{post.user}</p>
            </div>

            <img src={post.image} className="w-full h-72 object-cover" />

            <div className="p-3">
              <div className="flex gap-3 items-center">
                <Heart
                  onClick={() => toggleLike(post.id)}
                  className={`w-6 h-6 cursor-pointer ${post.liked ? "fill-red-500 text-red-500" : ""}`}
                />
                <MessageCircle className="w-6 h-6" />
              </div>

              <p className="mt-2 font-semibold">{post.likes} likes</p>
              <p className="text-sm">
                <span className="font-semibold">{post.user}</span> {post.caption}
              </p>
            </div>
          </CardContent>
        </Card>
      ))}

      {/* Bottom Nav */}
      <div className="fixed bottom-0 left-0 right-0 flex justify-around p-3 border-t bg-white">
        <HomeIcon />
        <SearchIcon />
        <Plus className="w-6 h-6" />
        <Heart className="w-6 h-6" />
        <User className="w-6 h-6" />
      </div>
    </div>
  );
}

function HomeIcon() {
  return <div className="w-6 h-6 bg-black rounded-sm" />;
}
function SearchIcon() {
  return <div className="w-6 h-6 border border-black rounded-full" />;
}
