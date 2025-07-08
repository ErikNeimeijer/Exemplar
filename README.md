// EXEMPLAR WEBSITE — VOLLEDIGE WERKENDE STRUCTUUR

import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Upload, ThumbsUp, Music } from "lucide-react";

const dummyFilms = [
  {
    id: 1,
    title: "The Godfather",
    year: 1972,
    exemplarStill: "/stills/godfather.jpg",
    exemplarMusic: "/music/godfather.mp3",
    uploads: 5,
    votes: 124,
    musicVotes: 89,
  },
  {
    id: 2,
    title: "Inception",
    year: 2010,
    exemplarStill: "/stills/inception.jpg",
    exemplarMusic: "/music/inception.mp3",
    uploads: 8,
    votes: 97,
    musicVotes: 76,
  },
];

export default function Exemplar() {
  const [films, setFilms] = useState(dummyFilms);

  const handleVote = (id, type) => {
    setFilms((prev) =>
      prev.map((film) => {
        if (film.id === id) {
          return {
            ...film,
            votes: type === "still" ? film.votes + 1 : film.votes,
            musicVotes: type === "music" ? film.musicVotes + 1 : film.musicVotes,
          };
        }
        return film;
      })
    );
  };

  return (
    <div className="p-6 max-w-5xl mx-auto">
      <h1 className="text-3xl font-bold mb-4">🎬 Exemplar</h1>
      <p className="mb-6 text-muted-foreground">
        Kies de still en soundtrack die een film het best representeren – upload, stem, en bepaal het gezicht en geluid van de film.
      </p>
      <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
        {films.map((film) => (
          <Card key={film.id}>
            <CardContent className="p-4">
              <h2 className="text-xl font-semibold mb-1">{film.title} ({film.year})</h2>
              <img
                src={film.exemplarStill}
                alt={`Exemplar still for ${film.title}`}
                className="w-full h-56 object-cover rounded-xl my-2"
              />
              <audio controls className="w-full my-2">
                <source src={film.exemplarMusic} type="audio/mpeg" />
                Your browser does not support the audio element.
              </audio>
              <div className="flex justify-between items-center mt-4">
                <Button variant="outline">
                  <Upload className="w-4 h-4 mr-2" /> Nieuwe still
                </Button>
                <Button variant="ghost" onClick={() => handleVote(film.id, "still")}>
                  <ThumbsUp className="w-4 h-4 mr-1" /> {film.votes}
                </Button>
              </div>
              <div className="flex justify-between items-center mt-2">
                <Button variant="outline">
                  <Music className="w-4 h-4 mr-2" /> Upload muziekfragment
                </Button>
                <Button variant="ghost" onClick={() => handleVote(film.id, "music")}>
                  <ThumbsUp className="w-4 h-4 mr-1" /> {film.musicVotes}
                </Button>
              </div>
            </CardContent>
          </Card>
        ))}
      </div>
    </div>
  );
}
